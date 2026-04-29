# Feature Spec Discipline

> **The problem this solves**: 4-file structure (GOALS/STATE/DECISIONS/HEALTH)は
> WHY と WHAT-changed の層しか持たない。「この機能はどう振る舞うべきか」という
> 機能の契約書は別ファイルが必要。

This document specifies how Synapse Arrows projects keep machine-readable
feature contracts in `docs/specs/`.

## Why a separate layer

| 質問 | どこで答える |
|---|---|
| なぜこの機能を持つのか | GOALS.md |
| 先週どこを変えたか | STATE.md / DECISIONS.md |
| この設計を選んだ理由 | DECISIONS.md / Linksee Memory |
| **どのDB→どのプロンプト→どのモデルで応答するか** | **`docs/specs/{feature}.md`** |
| **「該当なし」のときの応答テンプレ** | **`docs/specs/{feature}.md`** |
| **編集チップに編集ボタンが必須か** | **`docs/specs/{feature}.md`** |

下3つが **機能仕様 (feature spec)**。これがないと、Claude はセッション毎に
「コードを読んで再構築する」ことになり、ScaNaviの「直したらまた壊れる」現象の
**第二の原因** になる。

## Spec-driven development との違い

| | Spec-driven dev (Harper Reed系) | Feature spec discipline (本書) |
|---|---|---|
| 用途 | **生成前** に書く | **保守時** に維持する |
| 寿命 | 一過性、生成後は削除も可 | 機能と同じだけ生き続ける |
| 読み手 | 生成時の Claude | 保守時の Claude + 人間 + reconnaissance ant |
| 場所 | プロジェクト直下 / 一時 | `docs/specs/` に永続 |

両立する。両方持っていい。

## File location and naming

```
{project}/docs/specs/
├── chat-recommendation.md       # 機能名で1ファイル
├── chat-detail-lookup.md
├── intent-classification.md
├── data-flow-recommended.md     # 機能横断のフロー
├── llm-role-routing.md          # 機能横断のポリシー
└── chat-ui.md                   # UI仕様
```

1機能1ファイル原則。横断するものは「-flow」「-routing」等の接尾辞。

## Required structure

実装テンプレ: [`05-templates/feature-spec.md.template`](../05-templates/feature-spec.md.template)

最低限の8項目:

1. **Purpose** (1 sentence) — ユーザーが何を達成するための機能か
2. **User Inputs** — 入力形式、例、エッジケース
3. **Data Sources** — 読み書きするテーブル / API / カラム
4. **LLM Roles** — どのモデルがどの役割を担うか + プロンプト要約
5. **Response Patterns** — 該当あり / 該当なし / API error / rate limit
6. **UI States** — loading / empty / error / success / partial
7. **Edge Cases** (regression-prone) — 必ず regression test に対応する記述
8. **Linked** — DECISIONS.md, Linksee caveats, テスト, コードへのリンク

## Status tagging

各ファイル先頭:

```markdown
Status: 🟢 stable / 🟡 evolving / 🔴 broken
Last reviewed: YYYY-MM-DD by {who}
```

- 🟢 stable: この記述に反する PR は基本却下
- 🟡 evolving: 進行中、レビュー時に注意
- 🔴 broken: 既知の壊れ、修正PR welcome

## Operating rules

### Rule 1: PR must update spec

機能のコードを変更する PR は、対応する spec doc を **同じPRで** 更新する。
さもなくば PR description で `[no-spec-change: <reason>]` を明示。

CIで強制:

```yaml
# .github/workflows/spec-sync-check.yml
- if: changed src/features/chat/* and not docs/specs/chat-*.md
  run: |
    if ! grep -q "\[no-spec-change:" $PR_BODY; then
      exit 1
    fi
```

### Rule 2: One feature, one file

横断する設計（例: LLM routing）は別ファイルに切り出す。1ファイルに2機能を
詰め込まない（spec肥大化が読まれなくなる第一の原因）。

### Rule 3: WHY は Linksee, WHAT は spec

- Spec doc に書くのは **WHAT**: どう振る舞うか
- WHY（なぜこの設計を選んだか）は Linksee Memory の goal/context layer に
- これにより spec が肥大化せず、純粋な仕様書として読める

### Rule 4: reconnaissance ant が読む

[reconnaissance-ant](./reconnaissance-ant.md) が `docs/specs/` を読み、
本番挙動と spec の乖離を検出する。spec は機械可読である必要があるため:

- 応答テンプレートは fenced code block で囲む
- 数値（文字数、ms 等）は明確に書く
- 「だいたい」「適切に」のような曖昧表現を避ける

### Rule 5: Spec breaking change は DECISIONS.md エントリ必須

🟢 stable な spec を変更するときは:

1. PR description に `[spec-breaking: <feature>]`
2. DECISIONS.md エントリ（reason / reversibility / migration）
3. Linksee Memory に caveat: 「以前の spec で運用していて XX 問題」
4. レビュアー1人以上の明示的承認

## Adoption order for existing projects

ScaNaviの場合:

### Phase 1: 既存挙動の凍結（Day 1-2）
- [ ] `docs/specs/chat-ui.md` — 現在の編集チップ仕様、画面レイアウト
- [ ] `docs/specs/chat-recommendation.md` — 推薦応答パターン
- [ ] `docs/specs/llm-role-routing.md` — Sonnet/Haiku/templateの責任範囲

### Phase 2: 拡張（Week 1）
- [ ] `docs/specs/data-flow-recommended.md`
- [ ] `docs/specs/intent-classification.md`

### Phase 3: 強制（Week 2）
- [ ] `.github/workflows/spec-sync-check.yml` 追加
- [ ] reconnaissance-ant が specs/ を読み始める

## Anti-patterns

- **Spec が docs/SPEC.md 1ファイルに全部書いてある**: 検索性が崩壊する。1機能1ファイル
- **WHY も spec に書く**: spec が論文化して読まれなくなる。WHY は Linksee に
- **🟢 stable をつけて運用しない**: 全部🟡で「いつでも変えていい」状態は、結局
  spec を持っていないのと同じ
- **過度に詳細化**: 8項目以上に拡張すると読まれない。それ以上書きたい衝動は
  Linksee に流す
- **コードからspec生成**: できるが推奨しない。spec は **意図** を持つべきで、
  コードの逆プロパゲーションだと意図が消える

---

## See also

- [scope-locks.md](./scope-locks.md) — spec と一致しない変更を物理的に止める層
- [reconnaissance-ant.md](./reconnaissance-ant.md) — spec と本番挙動の乖離を
  毎朝検出する層
- [4-file-structure.md](./4-file-structure.md) — WHAT-changed の層との関係
- [`05-templates/feature-spec.md.template`](../05-templates/feature-spec.md.template)
