# Reconnaissance Ant Pattern

> **The problem this solves**: コードレベルのscope-locksは「明示的に凍結したもの」
> しか守れない。パフォーマンス劣化、横断UX一貫性、未発見の応答崩れ等は通る。
> KanseiLINKを内向きに使い、毎朝全プロダクトをcrawlしてdriftを発見する。

This file documents the **offensive (active) half** of Synapse Arrows'
two-layer protection model. The **defensive (passive) half** is
[scope-locks](./scope-locks.md).

## What

KanseiLINK の MCP ツール群（`take_snapshot`, `evaluate_design`,
`agent_voice`, `audit_cost`, `search_services`）を **社内プロダクトに毎朝
当てる** crawler agent。検出した drift を STATE.md / Linksee Memory /
朝ダイジェストに流す。

## Why this layer

scope-locks では捕まらない drift:

| Drift type | scope-locksで捕まる？ | reconnaissance-antで捕まる？ |
|---|---|---|
| ロックしたUIファイルの編集 | ✅ | ✅ (重複) |
| ピクセル単位の劣化（ロック対象外） | ❌ | ✅ |
| 応答時間のじわじわ増加 | ❌ | ✅ |
| 横断プロダクトでの単語表記揺れ | ❌ | ✅ |
| 新しい入力で応答パターンが崩れる | ❌ | ✅ |
| LLMコストが想定baselineを超える | ❌ | ✅ |
| 本番URL の HTTP 5xx | ❌（CIは検出しない） | ✅ |
| 既知ファイルへの不正編集 | ✅ | ❌（このlayerが見るのは出力側） |

**両層が必要。** scope-locks は入力側（コード変更）を、reconnaissance-ant は
出力側（本番挙動）を見る。

## Why KanseiLINK内向きに使うのか（戦略的価値）

これは単なる監視層ではなく **GTM資産**:

1. **ドッグフード²**: KanseiLINKが他社向けに売るツールを、まず自社プロダクト群
   に毎日当てる。販売トークの最強の証拠 ——「我々は自社全プロダクトに毎朝
   これを当てています」
2. **self-similar architecture の体現**: 同じツール（KanseiLINK）が
   company-OS と product-OS の両層で動く。Playbookの principle そのもの
3. **Synapse Threads MCP との接続**: 偵察結果を各プロダクトの Cofounder
   Claude に直接 ping できる土台
4. **記事ネタ**: 「Synapse Arrows の全プロダクトは KanseiLINK が監視している」
   は Zenn / Dev.to で書ける

## Configuration

各プロダクトで `reconnaissance-config.json` を持つ:

```json
{
  "$schema_version": 1,
  "product": "ScaNavi",
  "schedule": "0 9 * * *",
  "monitors": {
    "snapshot": {
      "urls": ["https://sca-navi.com/", "https://sca-navi.com/chat"],
      "diff_threshold_pct": 5
    },
    "agent_voice_probe": {
      "questions": [
        "辛口の重いの",
        "華やかで甘いやつ",
        "ペアリング: 寿司",
        "どぶろくありますか",
        "[該当なしを引き出すための入力]"
      ],
      "expected_patterns": "docs/specs/chat-recommendation.md"
    },
    "perf_baseline": {
      "ttfb_ms_max": 800,
      "ttf_response_ms_max": 4000
    },
    "design_lock_check": {
      "lock_file": "design.lock.json"
    },
    "cost_baseline": {
      "daily_llm_usd_max": 5.0
    }
  },
  "report_to": ["STATE.md", "Linksee Memory", "morning_digest"],
  "urgency": {
    "snapshot diff > 10%": "critical",
    "ttfb > 2x baseline": "critical",
    "agent_voice unexpected pattern (1 of N)": "warning",
    "agent_voice unexpected pattern (3+ of N)": "critical"
  }
}
```

実装テンプレ: [`05-templates/reconnaissance-config.json.template`](../05-templates/reconnaissance-config.json.template)

## Reporting tiers

| Tier | 条件 | アクション |
|---|---|---|
| 🟢 No drift | 全項目pass | STATE.md に「OK」のみ追記 |
| 🟡 Minor drift | 1項目fail、3日以内に解消可能と思われる | STATE.md + Linksee context layer |
| 🔴 Critical | 即時対応必要（critical urgencyに該当） | + 朝digest + Slack/メール |

3日連続で🟡 → 自動的に🔴に昇格。

## What it crawls (per product, per morning)

```
┌─────────────────────────────────────┐
│  Cron: 09:00 JST                     │
└──────────────┬──────────────────────┘
               │
               ▼
For each product in [KanseiLink, AgentStars, ScaNavi, CardWize, Linksee Memory]:

  1. take_snapshot (UI clone)
     → 前日との pixel diff
     → diff > threshold なら 🔴

  2. urls_must_200 ping (HEALTH.json から読込)
     → 5xx なら 🔴

  3. evaluate_design vs design.lock.json
     → frozen_components の値が乖離なら 🔴

  4. agent_voice probe
     - 既知の質問N本を投げる
     - 応答パターンが docs/specs/{feature}.md と乖離していないか
     - 言語、トーン、構造、文字数

  5. perf baseline check
     - 応答時間 / TTFB / time-to-first-token

  6. cost baseline check (audit_cost)
     - 過去7日のLLMコストvs baseline

  7. cross-product UX consistency
     - 同じ概念の表記揺れ（例: ScaNaviで「銘柄」、KanseiLinkで「ブランド」）
     - 同じ操作の手数差
```

## Implementation roadmap

Tier-based, not week-based. Pick up Tier B when the trigger condition is
met — don't pre-schedule.

### Tier A: foundation (do whenever) — ~1 day total
- [ ] `reconnaissance-config.json` template と schema 確定 (✅ done in v0.2)
- [ ] HEALTH.json から urls_must_200 を読込む形を確定
- [ ] KanseiLINK 既存ツールの「内向き呼び出し」モードを追加 (~半日)

### Tier B: MVP (trigger: post-launch slack day) — ~2-3 days total
- [ ] Cron orchestrator: KanseiLINK 内に新規エンドポイント
- [ ] Snapshot diff（前日との比較ロジック）
- [ ] agent_voice probe runner
- [ ] STATE.md 自動追記スクリプト
- [ ] 朝digest連携（Linksee Memory経由）
- [ ] 最初の被験者: ScaNavi + AgentStars 2 本で開始

### Tier C: full coverage (trigger: MVP stable for 1 week) — ~1 day
- [ ] CardWize, KanseiLink, Linksee Memory の config 追加
- [ ] Visual regression baseline 作成
- [ ] False positive 率の計測（< 5% 確認まで dry-run）

### Tier D: external storytelling (trigger: full coverage stable) — ~1 day
- [ ] Zenn 記事 1本: "We let KanseiLINK monitor itself every morning"
- [ ] Dev.to 翻訳版
- [ ] X で展開

## Anti-patterns

- **False positive を放置する**: 偵察アリの信頼度が下がると無視される。
  W3 dry-run 期間で false positive 率 < 5% を確認してから本格運用へ
- **全プロダクトに同時導入**: 1-2 product でMVP→学習→拡大、の順を守る
- **monitorsを増やしすぎる**: 上記7項目以上を一度に入れない。各項目の
  baseline confidence が育ってから次を足す
- **手動運用を続ける**: 「毎朝チェックする」を人間がやるとサボる。Cron化必須
- **報告先がgit logだけ**: STATE.md / Linksee / digest の3点同時に流すこと
  （見落としを防ぐ）

## Synapse Threads MCP との接続（Tier C+ / future）

reconnaissance-ant が🔴を検出したとき、現状は「人間が読む」ところで止まる。
将来的には:

```
ant detects critical drift
  → posts to Synapse Threads MCP
    → ScaNavi Cofounder Claude が pickup
      → Implementer Claude にチケット渡す
        → 修正PR が自動draft
```

これが完成すれば **Synapse Arrows = 完全自走するOSが動くプロダクト群**
として外部に説明できる。

---

## See also

- [scope-locks.md](./scope-locks.md) — 受動的な防壁（既知の契約を守る）
- [4-file-structure.md](./4-file-structure.md) — 偵察結果の流れ込み先
- [`04-tooling-gaps/02-kansei-link-as-internal-monitoring.md`](../04-tooling-gaps/02-kansei-link-as-internal-monitoring.md)
  — KanseiLINK内向き運用の戦略的価値とGTM
- [`03-tools/linksee-memory.md`](../03-tools/linksee-memory.md) — drift report
  の context/caveat layer 流入先
