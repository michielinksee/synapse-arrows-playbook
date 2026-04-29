# Scope Locks — Protecting What Has Been Decided

> **The problem this solves**: PR細切り規律だけでは「Claudeが周辺ファイルを
> ついで修正する癖」を止められない。物理的に編集スコープを制約する5層の
> 防御設計。

This file documents the **defensive (passive) half** of Synapse Arrows'
two-layer protection model. The **offensive (active) half** is the
[reconnaissance ant](./reconnaissance-ant.md), which finds drift the locks
cannot anticipate.

## Why this layer exists

ScaNavi 2026年4月の事象:

- 別Claude が PR を細切りに切る規律を守って実装した
- それでも各PRが **「ついでに」** 周辺UIを動かした
- 結果: チャット文言を直すたびに、固定したはずのUIが微妙に動く

これは規律の失敗ではなく、LLMの **構造的な癖**:

> 修正対象ファイルの周辺を読み込むと、「ここも整理した方がいい」と判断して
> 触る。過去の合意は「ファイルの中ではなく人間の頭の中」にあるので失われる。

したがって「触ってはいけないものは、コードレベルで触れないようにする」
必要がある。

## The 5 layers (weakest to strongest)

| 層 | 道具 | 検出タイミング | 強度 | 必要工数 |
|---|---|---|---|---|
| 1. 警告 | `// DANGER ZONE` コメント | 編集時の自己制止 | 弱 | 5min |
| 2. PR スコープ宣言 | PR template + scope-check workflow | PR作成時 | 中 | 1h |
| 3. ファイル凍結 | `.locked-paths` + pre-commit hook | コミット時 | 中強 | 2h |
| 4. デザイン契約 | `design.lock.json` + CI check | CI時 | 強 | 4h |
| 5. ピクセル検証 | Visual regression (Playwright Snapshot等) | CI時 | 最強 | 1d初期 |

各プロダクトは **少なくとも層1〜3を必須**、UI重視プロダクトは **層4〜5も必須**。

## Layer 1: DANGER ZONE comment

ファイル先頭やfragileな関数に:

```ts
// ============================================================
// DANGER ZONE — Last incident: 2026-04-XX, FIX-LOG.md entry
// Before editing this file, read docs/specs/{feature}.md
// and confirm with @michielinksee.
// ============================================================
```

すでにScaNaviのPR #48で導入済み。最低限の警告層、しかし強制力なし。

## Layer 2: PR scope declaration

PR description の冒頭に必須セクション:

```markdown
## Scope of this PR
- [x] Chat response logic
- [ ] UI components (DO NOT TOUCH)
- [ ] Database schema
- [ ] LLM model selection

## Files I expect to change
- src/features/chat/responses.ts
- src/features/chat/__tests__/responses.test.ts
```

`.github/workflows/scope-check.yml` が `git diff --name-only origin/main...HEAD`
の結果と PR description の Files セクションを比較し、宣言外の diff があれば
fail。

実装テンプレ: [`05-templates/pr-scope-template.md`](../05-templates/pr-scope-template.md)

## Layer 3: `.locked-paths` + pre-commit hook

repo直下の `.locked-paths`:

```
# Files that require explicit unlock to modify.
# Unlock by prefixing commit message with "[unlock: <reason>]"
# AND adding a DECISIONS.md entry.

src/components/chat/
src/styles/tokens.css
docs/specs/chat-ui.md
```

`.husky/pre-commit` がコミット時にチェック、unlock prefix がなければ reject。

実装テンプレ: [`05-templates/.locked-paths.template`](../05-templates/.locked-paths.template)

ロック解除手順:

1. 解除理由を整理（"why now"が明確であること）
2. 該当 commit message を `[unlock: chat-ui spec change for editable chips]` で開始
3. DECISIONS.md に新規エントリ追加（ロック解除理由 + 影響範囲）
4. レビュアー（最低1人）の明示的承認

## Layer 4: `design.lock.json`

色・余白・サイズ・凍結コンポーネント仕様を機械可読に:

```json
{
  "tokens": {
    "color.brand.primary": "#1a8fcb",
    "spacing.chat.bubble": "12px 16px"
  },
  "frozen_components": {
    "EditableSakeChip": {
      "must_have_edit_button": true,
      "must_have_remove_button": true,
      "must_allow_add_missing_sake": true
    }
  }
}
```

CIチェック:

- スタイルファイルが `tokens` を介さず生値（`#1a8fcb` 直書き）→ fail
- `frozen_components` の値が変わって DECISIONS.md エントリ無し → fail

実装テンプレ: [`05-templates/design.lock.json.template`](../05-templates/design.lock.json.template)

## Layer 5: Visual regression test

Playwright Snapshot もしくは Chromatic / Percy:

```ts
test('chat screen stays visually identical', async ({ page }) => {
  await page.goto('/chat');
  await expect(page).toHaveScreenshot('chat-empty.png');
  await page.fill('input', '辛口の重いの');
  await page.click('button[type=submit]');
  await expect(page).toHaveScreenshot('chat-recommendation.png');
});
```

ベースライン更新には人間の明示的承認が必要。**ピクセル単位で凍結が効く**。

ツール比較は [`04-tooling-gaps/01-visual-regression-stack.md`](../04-tooling-gaps/01-visual-regression-stack.md)

## Adoption checklist

新規プロジェクト立ち上げ時:

- [ ] `.locked-paths` ファイル作成（最低: `docs/specs/`, 主要UIディレクトリ）
- [ ] `.husky/pre-commit` に locked-paths guard 追加
- [ ] `.github/PULL_REQUEST_TEMPLATE.md` に scope宣言セクション追加
- [ ] `.github/workflows/scope-check.yml` 追加
- [ ] UI重視なら `design.lock.json` 初期化 + tokens への refactor
- [ ] UI重視なら Playwright Snapshot 5本以上

既存プロジェクト追加時の順序:

1. `.locked-paths` を **明らかに固定したい場所だけ** で開始（過剰指定は萎える）
2. 1-2週運用してロック解除頻度を観察
3. 安定したら層4へ拡張

## Anti-patterns

- **過剰ロック**: 全ディレクトリを `.locked-paths` に入れると、毎回 unlock が必要で開発が止まる。**「最後にユーザー合意した完成形」だけ** ロックする
- **ロック解除をDECISIONS.mdに書かない**: 解除はしたが理由が残らない → 次のClaudeセッションで「なぜここをロック外したんだっけ」が再発する
- **層4だけ入れて層3を入れない**: pre-commit gate なしで CI gate だけだと、ローカルで気づかず時間ロス
- **Visual regression を入れただけで安心する**: ベースライン更新を雑にやるとロックの意味が消える

## Promotion / demotion

- 層1 → 層2: 1回 incident → PR description 不在で同じファイルが壊れた
- 層2 → 層3: 1回 incident → PR description 内の宣言を破ってもCIが見逃した
- 層3 → 層4: 連続2回 incident → unlock prefix を雑につけて壊した
- 層4 → 層5: ピクセル単位の劣化が目視で発見された

降格は基本しない（一度入れた層は維持コストが軽いことが多い）。

## When this layer is not enough

scope-locksは「**既知の契約を守る**」ためのもの。次の状況では捕まえられない:

- パフォーマンスがじわじわ劣化する
- 横断プロダクトの UX 一貫性が崩れる
- 新しい入力パターンで応答が壊れる
- 凍結対象に **入れていなかった** 部分の劣化

これらは [reconnaissance ant](./reconnaissance-ant.md) が拾う領域。

---

## See also

- [reconnaissance-ant.md](./reconnaissance-ant.md) — 能動的に異常を探す層
- [feature-spec-discipline.md](./feature-spec-discipline.md) — 仕様書の書き方と運用
- [3-tier-boundaries.md](./3-tier-boundaries.md) — 行為レベルのboundaries（人間判断ベース）

scope-locks は3-tier-boundariesの **実装** に近い。boundariesが「何を ⚠️ にするか」を決め、scope-locks が「⚠️ 行為を **物理的に** 止める」役割。
