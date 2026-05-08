# Zenn pain-first writing playbook

> Status: 確立、 2026-05-08 起案
> Owner: Michie (writer) + Cofounder Claude (review / draft)
> Trigger: Michie 自己診断 (2026-05-08): 過去 10 記事で likes 1-2 / 記事、 Zenn は記事単位で viral 起こるが、 Michie の記事は 「何を解決した記事で、 ユーザーは何をどうすれば自分の困りごとが解決できる記事なのか分からない」 のがネック
> Companions: [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md), [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md)

## なぜ今までの Zenn 記事が刺さらなかったか

過去 10 記事の audience analysis:

| Audience | 世界の母数 | Michie の記事傾向 |
|---|---|---|
| MCP server **作る人** | ~数千人 (global) | 大半がこの層に向けた title / body |
| Claude Code / Cursor / Codex **使う人** | ~数十万人 (global) | これに向いた記事は少数 |

→ Michie は技術的に深いが audience size の小さい層に書いていた。 同じ Linksee Memory の話でも、 user 視点で書き直すと audience が **約 100x** 広がる。

## トレンド feed (2026-05-08 観測) から抽出した viral 構造 3 パターン

### 構造 1: 「あなたの X、 実は Y」 = surprise hook
- 例: 「あなたの Claude Code の WebFetch、 実は Web をちゃんと読んでいない」 → 232 ♡ (top of Tech feed)
- 1 行目で 「え、 私のことだ」 と読者が認識して click する
- X = ユーザーが日常使ってる固有名詞、 Y = 知らなかった事実

### 構造 2: 「X 入門」 / 「X 検証してみた」 = beginner / experiment
- 例: 「Claude Code ユーザーのための Codex 入門」 → 82 ♡
- 例: 「Claude Code に全部やらせる時代が来た のか検証してみた」 → 21 ♡
- beginner curriculum or experiment narrative

### 構造 3: 「X したら Y」 = concrete outcome
- 例: 「Claude Code の 5 時間制限を API 料金換算すると約 62 ドルだった」
- 例: 「Qwen が閉じ始めたので Gemma 4 を選んだ」
- 数字 / 結論 / 固有名詞を title に直接入れる

→ どれも **end user の pain × surprise / beginner approach / concrete outcome** のいずれかを満たす。

## Zenn pain-first playbook (鉄則)

### Title 鉄則
**以下のいずれか 1 つ以上を必ず satisfy** (両立すればなお良い):

1. **「あなたの X、 実は Y」** ← surprise hook
2. **「X したい人へ、 Y する Z 入門」** ← beginner audience marker
3. **「X したら Y (具体数字 / 結論)」** ← concrete number / outcome
4. **「X が Y になったので、 Z を試した」** ← situational pivot
5. **「X するために、 Y を作った」** ← clear deliverable
6. **「X しないために (こう設計した)」** ← anti-pattern guard

### Title 制約
- **70 字以内** (Zenn の hard limit、 第3弾で踏んだ罠)
- **safety target は 60 字以内** (10 字 buffer)
- **絵文字 1 個** を frontmatter で指定 (section icon として使われる)
- **固有名詞 1 つ以上** (Claude Code / Cursor / Codex / Gemini / MCP / Stripe / Vercel 等)
- **maker 視点ではなく user 視点で書く**: 「MCP server を作る方法」 ではなく 「Claude Code を便利にする方法」

### File 名 (= slug) 制約 ⚠️ 別ルール
Zenn は **ファイル名 (拡張子除く) = article slug**。 別途以下を満たす必要:

- **12〜50 文字** (Zenn hard limit、 第4弾で踏んだ罠)
- **半角英数 + ハイフン (-) + アンダースコア (_) のみ** (大文字・日本語・記号 NG)
- **safety target は 45 文字以下** (5 字 buffer)
- 命名パターン: `linksee-memory-{client}-{topic}-{YYYYMMDD}` (例: `linksee-memory-claude-code-recall-20260508` = 42 chars)
- topic 部分は **user benefit を表す動詞 / 名詞** (例: recall / publish / five-blocks / 6-layer)
- 既存 file 名と重複しない

### Body 構造 (上から下に厳守)

```
1. lead — ユーザーの frustration を 3-5 行で再現
   「こんな経験ありませんか?」 で始める or 具体的な月曜朝のシーンを描く

2. 体感 before / after — 5 行以内で対比
   会話のサンプル / コマンドの output 比較が effective

3. 原因の診断 — ここで初めて technical 用語 OK
   なぜそれが起きるのか、 仕組みレベルで 1-2 段落

4. 解決策 step-by-step — copy-paste 可能なコード入り
   reader が手元で再現できる手順、 各 step に title

5. つまづきポイント — 大抵 3 個
   「私はこう踏んだ」 を実体験として書く

6. TL;DR — 2-3 行で全部のまとめ
   reader が記事を read しなくても scan できる

7. 次のアクション — 1 行 command / link
   「今すぐ試したい人は npm install -g X」 のような明示的な next step
```

### キーワード戦略 (2026-05 現在の hot)

`topics` フロントマターに **3-5 個必ず** 設定。 hot keyword リスト:

- **claude** / **claudecode** (Claude Code、 常時 hot)
- **cursor** (高)
- **codex** (急上昇 — OpenAI CLI、 2025 年後半から)
- **gemini** / **geminicli** (中)
- **mcp** (高、 2025 後半から定着)
- **rag** (定番)
- **agent** / **aiagent** (常時 hot)
- **anthropic** / **openai** / **google** (vendor タグ)
- **typescript** / **python** / **rust** (技術 stack)
- **oss** / **npm** (distribution)

### 「trend が変わった瞬間」 を逃さない

新製品 / 新機能 / 大手の動きの **発表から 24-72h 以内に記事化**:
- 「OpenAI Codex 出た直後の入門」 → 数日で reach 拡大
- 「Anthropic Skill 発表の翌週」 → 検索流入大
- 「Gemini CLI が MCP 対応した瞬間」 → niche だが viral 余地

→ Cofounder Claude が news watch を兼ねて、 trend 検知時に Michie に「今書け」 trigger を出す。

## Anti-patterns (Michie の旧 10 記事に共通)

❌ **maker 視点 title**: "MCP tool registration patterns" — 作る人にしか刺さらない
❌ **product launch 単発記事**: "Linksee Memory 出した" だけだと共感の入口が無い
❌ **technical terms 先行 lead**: 1 行目から 「FTS5 trigram」 と言うと user は逃げる
❌ **解決策の前に説明が長い**: 仕組みは原因の診断 (step 3) に押し込み、 lead は frustration から
❌ **絵文字 / 構造マーカー無し**: 平らな text の壁、 scan しにくい
❌ **次のアクション欠落**: 読み終わって 「で、 何する?」 と reader を放置

## 既存 10 記事の retroactive 改題候補

| 現 file | 旧 title | 新 title 案 | 推奨 |
|---|---|---|---|
| linksee-memory-mcp-five-blocks-20260507 | あなたの MCP server、 実は Tools しか使ってない (5 blocks 全実装 / v0.3.0) | (現状維持、 maker-audience) — 並列で第4弾を user-audience で書く | 据置 |
| linksee-memory-claude-code-6-layer-20260422 | Claude Code の "session 記憶喪失" を解決する Linksee Memory を作った話 | (既に user-pain 寄り、 軽く polish 程度) | 軽 polish |
| linksee-memory-mcp-publish-glama-traps-20260506 | あなたの MCP server、 実は Glama listing で 3 週間止まる (5つの罠と解決策) | (既に viral pattern 通り、 触らない) | 据置 |
| kanseilink-mcp-tool-registration-20260415 | MCP tool registration patterns | **Claude Code に MCP tool を 0 から登録する完全ガイド (Codex / Cursor も同パターン)** | 改題 |
| kanseilink-fts5-trigram-cjk-20260507 | Weekly tech: SQLite FTS5 trigram for CJK search | **Claude Code が日本語ファイル名を検索できない問題 (SQLite FTS5 trigram で解決)** | 改題 |
| kanseilink-mcp-builder-tips-20260428 | Weekly tech: MCP builder tips | **MCP server を作る人が知らないと損する 5 つの API (annotations / next-tool / compact mode)** | 改題 |
| kanseilink-token-benchmark-20260416 | Weekly tech: token benchmark | **Claude Code の token を 86% 削った話 (read_smart で実測)** | 改題 |
| kanseilink-sqlite-wal-mcp-20260421 | Weekly tech: SQLite WAL MCP | **MCP server で SQLite を使うなら必ず WAL モードにすべき理由** | 改題 |
| kanseilink-aeo-ranking-q2-2026 | AEO ranking Q2 2026 | **Claude / GPT / Gemini が同じ SaaS を選ぶ確率を測ったら見えた事実 (Q2 2026)** | 改題 |
| kanseilink-setup-test-20260416 | (test article) | (削除推奨) | 削除 |

→ 改題は GitHub-sync で title だけ変えればいい (URL slug は file 名なので変わらず、 既存 link 生きる)。

## 今後の記事の approval gate (= scope-lock)

新規 Zenn 記事を draft する時、 commit 前に **以下 7 項目すべて** に ✅ が必要:

```
[ ] Title: 「あなたの X、 実は Y」 等の 6 パターンのいずれかを満たす
[ ] Title 文字数: 60 字以下 (= 70 字 hard limit から 10 字 buffer)
[ ] File 名 (slug): 半角英数+ハイフン/_、 12-50 字 (45 字以下安全)、 既存と重複なし
[ ] Topics: 3-5 個、 hot keyword 1 個以上含む
[ ] Body の lead: ユーザーの frustration から始まる (technical 用語の壁を作らない)
[ ] Body の構造: 7 sections (lead / before-after / 診断 / 手順 / 罠 / TL;DR / 次のアクション)
[ ] 次のアクション: copy-paste 可能なコマンド or link で reader を完結させる
```

これを守らない記事は publish しない (= scope-lock で防御)。

### Self-check 1-liner (commit 前に必ず実行)

```bash
node -e "
const title = 'あなたの ...';
const slug = 'linksee-memory-...';
console.log('title:', [...title].length, '/ 60 safety:', [...title].length <= 60 ? '✅' : '❌');
console.log('slug:', slug.length, '/ 12-50:', slug.length >= 12 && slug.length <= 50 ? '✅' : '❌');
"
```

## Ablation experiment (= 効果測定)

Cofounder Claude が新 playbook 適用前 / 適用後の likes 数を track:
- **対照群** (旧 maker-audience): 第1弾 / 第3弾 + 改題前の weekly-tech 系
- **介入群** (新 user-audience): 第4弾 (これから書く) + 改題後の weekly-tech 系
- **measurement**: 公開 7 日後の likes、 npm DL、 GitHub stars 増分
- 適用後 5 記事で再 review、 効果なければ playbook 自体を見直す

## まとめ

- **maker → user 視点** の framing 転換が最大の lever
- **「あなたの X、 実は Y」** は 232 ♡ の上位 viral 構造、 Michie の hook はもう半分機能してる
- **Body 構造 7 sections** の縛りで scan しやすさを担保
- **70 字 hard limit** と **60 字 safety target** で deploy 失敗を防ぐ
- **Hot keyword 3-5 個** を topics に必ず設定
- 適用後 5 記事で ablation review、 likes が 5x 出なければ pattern 見直し
