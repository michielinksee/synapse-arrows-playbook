# KanseiLINK as Internal Monitoring Layer

> Status: gap as of v0.2 (2026-04-29).
> Tier A foundation: ✅ templates and docs in v0.2.
> Tier B MVP: triggered post-4/28 launch, ~2-3 days when KanseiLINK
> has slack capacity. Don't pre-schedule.
>
> Synapse Arrows の全プロダクトを、KanseiLINK 自身に毎朝監視させる構想。
> [reconnaissance-ant](../02-process/reconnaissance-ant.md) の実装基盤。

## The thesis

KanseiLINK は他社向けに販売する MCP intelligence layer。同時に **Synapse
Arrows 全プロダクトの監視レイヤー** として内向きに使う。理由:

1. **ドッグフード²** — 他社に売るツールを毎朝自社に当てる、最強の証拠
2. **GTMストーリー** — "Our products are watched by KanseiLINK every morning"
3. **self-similar architecture** — 同じツールが company-OS と product-OS で動く
4. **コスト合理性** — 別途監視SaaSを契約せずに済む（DataDog ¥10,000+/mo回避）
5. **将来のSynapse Threads MCP接続** — drift→threads→implementer Claude の自走化

## Existing KanseiLINK tools usable internally

監視に使える既存MCPツール:

| ツール | 内向け用途 |
|---|---|
| `take_snapshot` | UIスナップショット、前日との pixel diff |
| `evaluate_design` | `design.lock.json` との整合性チェック |
| `agent_voice` | チャット応答パターンの probe（既知質問N本） |
| `read_agent_voices` | 応答ログ蓄積、トーン drift 検出 |
| `audit_cost` | LLMコスト baseline check |
| `search_services` | 横断検索（横断UX一貫性検出） |
| `record_event` | drift event の永続化 |
| `get_insights` | 過去N日の drift パターン分析 |

つまり **MVP に必要なツールはほぼ既にある**。新規追加は薄い orchestration 層。

## What needs to be built (Tier B, ~2-3 days)

### 1. Internal-mode auth
KanseiLINK API を「自社プロダクト監視モード」で叩くトークン体系。Public API
クォータと独立に。

### 2. Cron orchestrator
```
POST /internal/reconnaissance/run
  body: { "config_path": "scanavi/reconnaissance-config.json" }
```
社内 Cron（Railway / Vercel cron / GitHub Actions schedule）から叩く。

### 3. Snapshot diff engine
`take_snapshot` の結果を S3 もしくは Supabase storage に保存。前日と pixel diff。

### 4. Spec-aware probe
`docs/specs/chat-*.md` を読み、期待パターンと `agent_voice` 結果を比較。

### 5. Reporting bridges
Drift event を以下に流す:
- 各プロダクトの STATE.md（git commit）
- Linksee Memory の context layer
- 朝digest agent（Tier C — once 2+ products are reporting）

## Architecture sketch

```
┌──────────────────────────────────────────────────────────┐
│  Cron: 09:00 JST                                          │
│  → POST /internal/reconnaissance/run × 5 products        │
└──────────────┬───────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────┐
│  KanseiLINK Reconnaissance Orchestrator                  │
│                                                           │
│  for each monitor in config:                              │
│    → call existing KanseiLINK MCP tool                    │
│    → compare with baseline (yesterday / spec / lock)      │
│    → classify: 🟢 / 🟡 / 🔴                              │
│    → record_event                                          │
└──────────────┬───────────────────────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────────────────────┐
│  Reporters (parallel)                                     │
│  ├─ STATE.md updater (git commit per product)            │
│  ├─ Linksee Memory writer (context layer)                │
│  ├─ Morning digest aggregator                             │
│  └─ Slack/email pinger (🔴 only)                         │
└──────────────────────────────────────────────────────────┘
```

## Baseline strategy

各 monitor は baseline を持つ:

| Monitor | Baseline source | Update frequency |
|---|---|---|
| Snapshot | 前日のsnapshot | daily（人間承認なし） |
| Design lock | `design.lock.json` | 手動（DECISIONS.md経由） |
| Agent voice | `docs/specs/chat-*.md` | 手動（spec更新時） |
| Perf | rolling 7日 p95 | rolling |
| Cost | rolling 7日 p95 | rolling |

## False positive 管理

W3 dry-run 期間（1週間）で:
- 各 monitor の false positive 率を計測
- 5%超 の monitor は disable し、threshold を見直す
- 5%以下になってから本格運用

dry-runでは drift を検出しても **alert は出さない**、log のみ。

## Public-facing story

5月末公開記事のドラフトタイトル候補:

- "We let KanseiLINK monitor itself every morning"
- "Synapse Arrowsが自社の全プロダクトに毎朝KanseiLINKを当てている話"
- "Self-similar monitoring: when your monitoring tool is also a product you sell"

これらの記事は KanseiLINK の販売トークの **動く証拠** になる。

## What this is NOT

- ❌ 一般的な APM（Datadog / New Relic 代替ではない）
- ❌ Uptime monitoring 専用（urls_must_200は HEALTH.json で持つ）
- ❌ ログ集約ツール

KanseiLINK 内向き運用は **エージェント挙動と UX 一貫性** に特化。
APM/uptime は別レイヤー（Tier C で Better Uptime 等を検討）。

## Risks

| Risk | Mitigation |
|---|---|
| KanseiLINK 自身がダウン → 監視も止まる | KanseiLINK の HEALTH.json を別系で監視（Better Uptime） |
| Cost が想定超過 | `audit_cost` で日次LLMコスト上限、超過で自動停止 |
| 自社用機能が public API を圧迫 | internal-mode auth で quota 分離 |
| Spec と実装の乖離が積み上がる | feature-spec-discipline で PR毎に同期強制 |

## Adoption sequence

Tier-based, not week-based. Pick up Tier B when KanseiLINK has slack
capacity (post-4/28 launch).

### Tier A: foundation (✅ done in Playbook v0.2)
- [x] templates and design docs
- [x] reconnaissance-config schema

### Tier B: MVP (~2-3 days when ready)
- [ ] internal-mode auth
- [ ] Cron orchestrator skeleton
- [ ] Snapshot diff (ScaNavi のみ最初の被験者)
- [ ] STATE.md updater

### Tier C: expand (trigger: B stable for 1 week)
- [ ] AgentStars + CardWize 追加
- [ ] Spec-aware probe
- [ ] Linksee Memory bridge
- [ ] False-positive 率計測（< 5% で本格運用）

### Tier D: full coverage + alerts (trigger: C stable)
- [ ] KanseiLink + Linksee Memory 追加（5/5 products）
- [ ] Slack alerter
- [ ] 公開記事第一弾

### Future (no trigger yet)
- [ ] Synapse Threads MCP との接続（drift→threads→implementer Claude）
- [ ] 外部公開（他のSolo Founder向けに自社プロダクト監視SaaSとして提供？）

---

## See also

- [reconnaissance-ant.md](../02-process/reconnaissance-ant.md) — 運用ドクトリン
- [scope-locks.md](../02-process/scope-locks.md) — 相補的な防御層
- [feature-spec-discipline.md](../02-process/feature-spec-discipline.md) — spec比較の参照元
- [`05-templates/reconnaissance-config.json.template`](../05-templates/reconnaissance-config.json.template)
