# Tokyo Conference 6/10 — Strategy + Backup Plans

> Status: 策定中、 2026-05-07 起案
> Conference: Code with Claude — Tokyo, 2026-06-10
> Days remaining: ~34 days (5/7 → 6/10)
> Owner: Michie (現地参加 + 営業) + Cofounder Claude (戦略 / 物量)
> Companions: [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md), [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md)

## Why this conference matters

Anthropic 主催の Tokyo conference はおそらく 2026 年で **アジア最大の Claude / MCP イベント**。
Boris Cherny (Head of Claude Code) / Ami Vora (Head of Product) / Angela Jiang (API/SDK Product Lead) クラスが登壇。
Synapse Arrows にとって:

1. **Linksee Memory Pro tier launch のタイミング** (4週間 sprint の最後尾)
2. **KanseiLink finance vertical の最初の anchor customer 探し**
3. **Anthropic eng 直接接点** (将来 acquisition / partnership で効く)
4. **Glama maintainer (punkpeye) + Composio 関係者と直接話せる可能性**

3週間後 = **3つの product strategy 全部の "first contact" タイミング**。 ここで何かが起きると、その後の 6か月加速する。

## Reality check — 公式 talk 枠は厳しい

### 通常の Anthropic conference の speaker 確定 timing

Code with Claude 系イベントの speaker lineup は通常 **2-3か月前 lock**。 5/7 時点で 6/10 conference には残り 34日 = ほぼ確実に主要枠は closed。

### 残された4 path

| Path | 確率 | 効果 | 工数 | Owner |
|---|---|---|---|---|
| **A. 公式 talk submission** | 5-10% | 高 (登壇者として brand) | 小 (申請のみ) | Michie + Cofounder |
| **B. Lightning talk / sponsor 枠 申請** | 15-25% (有料) | 中 | 小 | Michie |
| **C. Demo / community slot 申請** | 30-40% | 中 | 小 | Michie |
| **D. Side event 主催** (前夜 or after) | **70%** (自分で動ける) | 中〜高 | 中 | Michie + Cofounder |

→ **D を main、 A-C は parallel に申請** が現実解。

## Path D — Side event 主催 (主戦略)

### Concept

```
タイトル: "Synapse Arrows × Linksee Memory — Demo Night"
副題: "5 MCP blocks 全実装事例 / 日本 finance vertical / Solo founder の OS architecture"
日時: 6月10日 (火) 19:00-21:30 (Conference 終了直後)
       or 6月9日 (月) 19:00-21:30 (前夜祭、参加者来日済)
場所: Tokyo (会場決定: WeWork / Anthropic オフィス近く / 友人企業 / 飲食店個室)
形式: パネル + Demo + Networking
規模: 20-50人
費用: 飲み物軽食 ¥30K-50K (個人負担可能 範囲)
募集: X / Zenn / Conference 参加者向け DM
```

### Agenda (90 min program)

```
19:00-19:10  受付 + 自己紹介ボード (各人の興味タグ付け)
19:10-19:20  Synapse Arrows 全体 pitch (Michie)
              "Solo founder + 5 product + Self-similar OS architecture"
19:20-19:35  Linksee Memory v0.3 demo
              "5 MCP blocks 全実装事例 — 業界初"
              実 demo: Resources / Sampling / Server-side Agent Loop / Elicitation / Roots
19:35-19:50  KanseiLink finance vertical pivot pitch
              "Anthropic global tools の Japan ブリッジ"
              実 demo: J-GAAP Earnings Reviewer (TDnet 開示 → AI summary)
19:50-20:00  Synapse Arrows Playbook 紹介 (Public OSS doc)
              "Solo founder の operating system"
20:00-20:30  Lightning Talk 募集枠 (5min × 4-5人)
              参加者から「自分の MCP 実装事例」を拾う
20:30-21:30  Networking
              tech 立ち話 + finance / accounting professional との接続
```

### Why this works

- **公式 talk せずとも、conference 参加者の dense network に直接 access**
- **Anthropic eng / punkpeye / Composio / 日本 dev コミュニティ 全員候補**
- **Synapse Arrows brand を一夜で確立**
- **anchor customer 候補との face-to-face**

### 実施リスク

| Risk | Mitigation |
|---|---|
| 集客失敗 (5人未満) | 早期から Conference 参加者にリーチ + 友人 backup ride |
| Conference 当日疲労 | 前夜開催 (6/9) を選ぶと体力温存 |
| Anthropic 側に怒られる (公式に近すぎる名前) | "Synapse Arrows community gathering" 等にする |
| 場所予約ミス | 5月半ば確定 |

## Path A — 公式 talk submission

低確率だが試す価値あり。Submit 締切までに以下:

### Submission 文面 (英語)

```
Title: "Beyond Tools: Implementing All 5 MCP Blocks in Linksee Memory"

Abstract (250 words):
Most MCP servers today implement only Tools. Yet the MCP specification offers
five functional blocks — Tools, Prompts, Resources, Sampling, and Roots —
plus newer primitives like Elicitation, Async Tasks, and Server-side Agent Loops.

This talk presents Linksee Memory, a local-first MCP server that implements
all five core blocks plus the new Async + Sampling + Elicitation primitives.
We will demonstrate how the server orchestrates an autonomous memory consolidation
agent loop using the client's AI tokens (Sampling), with no server-side API
costs, while preserving privacy through local storage.

We will share concrete implementation patterns, the architectural trade-offs
we encountered (e.g., when to use Resources vs Tools), and three workflows
that became possible only after moving beyond Tools-only design:

1. Cross-session memory consolidation via Server-side Agent Loops
2. Out-of-band entity merge confirmation via Elicitation
3. RAG-style memory retrieval via streaming Resources

Linksee Memory has 1,900+ npm downloads in 3 weeks since launch, and serves
as the first reference implementation of the post-November 2025 spec primitives
in the local-first memory MCP space.

Speaker: Michie Yamaguchi, Solo founder of Synapse Arrows PTE. LTD.
         Singapore-based, builds 5 MCP-native products.
         Public Playbook: github.com/michielinksee/synapse-arrows-playbook

Length: 30 minutes (talk) + 15 minutes (Q&A)
```

### Submission 経路

```
1. claude.com/code-with-claude → speaker submission form 探す
2. もしくは X / LinkedIn DM:
   - Boris Cherny (@bcherny)
   - Anthropic Tokyo team
   - Conference organizer (DM 経由で submission 経路問い合わせ)
3. CC: Synapse Arrows Playbook URL (= "I have public methodology")
```

## Path B — Sponsor / Lightning Talk 枠

有料枠だが安定的。費用 vs benefit を判断:

### 想定費用

- Sponsor 個人 / startup tier: ¥100K-300K
- Lightning talk 5 min: included or ¥50K-100K
- Booth (machine demo + 1日説明): ¥200K-500K

### Decide criteria

```
予算 < ¥100K (= solo founder 範囲): pass
予算 ¥100K-300K (= validation 投資): consider lightning talk
予算 > ¥300K (= raise 後): consider booth
```

→ 現状 (bootstrap) は **pass + Path D 集中** が妥当。 funding / pilot revenue 入った段階で次回検討。

## Path C — Demo / Community slot

Anthropic コミュニティ系 conference では「demo 1分」「community announcement」枠が用意されることが多い。 公式 talk より application 容易。

### 試す手順

1. Conference page で "demo" / "community" slot の有無確認
2. 申請 form あれば即 submit
3. なければ Anthropic Tokyo team に直接 DM で問い合わせ

```
Hi Anthropic Tokyo team,

I'm Michie Yamaguchi from Synapse Arrows (Singapore). I've built Linksee Memory,
a local-first MCP server with 1,900+ downloads. For Code with Claude Tokyo,
I'd love to do a 5-minute demo of "all 5 MCP blocks fully implemented" —
ideally as a community slot or lightning demo.

If there is no formal slot, I'm also organizing a side event the same week
that may be of interest to attendees.

Thanks!
Michie
```

## Pitch deck 構成 (Tokyo 用 Synapse Arrows v1)

Conference 当日 + side event + 一対一営業で使う共通 deck。

### Slide 構成 (12-15 slides)

```
1. Title: "Synapse Arrows — A Solo Founder's MCP-Native OS"
   subtitle: "5 products, 1 operating system, public playbook"
2. The story: 4か月前まで普通の Solo dev 問題 → 5 product OS
3. Linksee Memory: local-first 6-layer memory (1,903 DL)
4. KanseiLink: Japanese SaaS intelligence (200+ catalog)
5. ScaNavi: vertical sake recommendation
6. CardWize: vertical credit card optimization
7. ReviewLens: vertical cosmetics review
8. The OS: Synapse Arrows Playbook (public)
   "Same OS at every scale: company → product → embedded agent → user"
9. Today's milestone: Linksee Memory v0.3 = 5 MCP blocks 全実装
10. Today's pivot: KanseiLink finance vertical = Anthropic 補完
11. The 12-month plan: $10K MRR (bootstrap) → $100K → ?
12. Why now: Tokyo at the inflection point
13. Ask: pilot customers / dev contributors / partnership
14. Contact: Michie / synapsearrows.com / linksee.com / kansei-link.com
15. Q&A
```

### 1-pager handout

A4 1枚、両面:

```
Front:
  Synapse Arrows — Singapore-based, MCP-native, 5 products, public Playbook
  Logo + 5 product overview + traction numbers
  QR: synapsearrows.com

Back:
  Linksee Memory: 1,903 DL / 5 blocks 実装 / Pro tier $5/mo
  KanseiLink: Japanese SaaS catalog / Finance vertical specialized
  Tokyo demo night: 6/9 19:00 (location TBD)
  Contact: Michie Yamaguchi / @ELLECraftsinga1
```

### 名刺 (英文)

```
Michie Yamaguchi
Founder, Synapse Arrows PTE. LTD.
Singapore

Linksee Memory · KanseiLink · ScaNavi · CardWize · ReviewLens
synapsearrows.com / linksee.com / kansei-link.com

X: @ELLECraftsinga1
GitHub: @michielinksee
```

## Networking strategy

### Pre-conference reach (5月後半)

- X で「Tokyo Conf 6/10 行きます、 Demo Night 主催します」 thread 投下
- Anthropic Tokyo team に follow + DM
- Boris Cherny / Ami Vora / Angela Jiang に X follow + 軽い engagement
- punkpeye (Glama) に「Conference 行きますか?」 DM
- Composio 日本担当 (もしいれば) reach
- 既存 Linksee Memory user で Tokyo 在住者を探して invite

### Conference day

- 名刺持参 50枚
- 1-pager 30枚
- Linksee Memory demo 用 laptop 持参
- スマホで Linksee Memory mobile (将来) も
- 会場で 10-20人と直接会話、 X handle 交換

### Demo Night (6/9 or 6/10 夜)

- 名刺持参
- 1-pager 持参
- demo laptop x 2 (backup含む)
- KanseiLink finance demo data 用意 (上場企業の TDnet 開示 sample 1社分)
- 飲食物発注

### Post-conference follow-up routine

```
Day 0 (Conference 当日 夜):
  会った全員に X 上で軽い「ありがとう」 DM (or follow + reply)

Day 1 (Conference 翌日):
  特に深く話した人 5-10人に個別 long-form DM:
    "デモした Linksee Memory / KanseiLink について追加情報"

Day 7:
  pilot 候補 (会計事務所 etc) に formal proposal メール
  Linksee Memory waitlist signup を依頼

Day 14:
  Conference 全体振り返り Zenn 記事
  "Code with Claude Tokyo で会った 5つの surprise"
  自分のブランド資産化
```

## Pre-Tokyo Sprint (5月W2-W4 + 6月W1)

Tokyo Conference 直前までに揃えたいもの (4 weeks):

```
Week 1 (5/12-5/18):
  - Linksee Memory Resources 実装
  - KanseiLink ICP-A list 5社
  - Side event 場所 / 日時 確定

Week 2 (5/19-5/25):
  - Linksee Memory Sampling + Server-side Agent Loop
  - KanseiLink J-GAAP Earnings Reviewer demo build start
  - Pitch deck v1 / 1-pager / 名刺発注

Week 3 (5/26-6/1):
  - Linksee Memory Elicitation + 日英 bilingual
  - J-GAAP Earnings Reviewer demo 完成
  - Side event 募集開始 (X / Zenn)
  - Anthropic Tokyo team 個別 reach

Week 4 (6/2-6/8):
  - Linksee Memory Pro tier landing page launch
  - Stripe 接続 + 30日 trial 設定
  - Synapse Arrows Playbook v0.3 公開 (この doc 含む 3本)
  - Side event 出席者数確認 + pizza 発注
```

## Success metrics (Tokyo Conference 期間)

| KPI | Min target | Stretch |
|---|---|---|
| Demo Night 参加者 | 20人 | 50人 |
| 名刺交換 | 30人 | 80人 |
| Linksee Memory waitlist signup (Tokyo由来) | 50人 | 150人 |
| KanseiLink pilot interest 取得 | 1社 | 3社 |
| Anthropic eng 直接接点 | 1人 | 5人 |
| Press / blog mention | 0 | 1-2本 |
| Synapse Arrows Playbook GitHub stars | +20 | +100 |

## Anti-patterns

- **Demo Night を Anthropic 公式と誤認させる名前** → 商標 / 法的 risk
- **Pitch deck を生 sales 化** → 警戒される、教育 / 共有姿勢で
- **Anthropic / Composio を批判** → community 内で評判悪化
- **酒飲みすぎ** → 翌朝 follow up メール飛ぶ
- **Side event 投資ゼロ** → 軽く ¥30K でも飲み物軽食必要

## Decision log

### 2026-05-07 — Tokyo Conference D 主軸戦略決定

**CONTEXT**:
公式 talk 枠 ほぼ closed (1か月前)。 Synapse Arrows brand を Tokyo conf で立てるには代替が必要。

**DECISION**:
- Path D (Side event 主催) が main、A-C を parallel attempt
- Linksee Memory Pro tier launch を Conference 直前に時系列 align (6/8 launch)
- KanseiLink Finance vertical demo を Tokyo で初公開
- Synapse Arrows Playbook v0.3 (3 docs) を Conference 直前公開

**REASON**:
- 1か月では公式枠取得困難
- D は自分で controll 可能 + dense network access
- Linksee Memory + KanseiLink + Playbook 3点同時公開で brand 構築

**REVERSIBILITY**:
High — Side event は 1週間前まで cancel 可能、 Pro tier launch も postpone 可能 (但し brand 機会失う)

**OPEN QUESTIONS**:
- Side event 場所 (WeWork / 友人企業 / 飲食店)
- 前夜 (6/9) か当日夜 (6/10) か
- ¥30K-50K の自己負担 vs sponsor 募集
- Demo Night co-host を募るか (e.g., punkpeye / Composio Japan rep)

## Companion docs

- Linksee Memory Pro tier 4-week sprint: [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md)
- KanseiLink Finance Vertical Pivot: [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md)

## Next actions (this week 5/7-5/14)

- [ ] Anthropic Tokyo team / Boris Cherny / Ami Vora に X follow + light engagement
- [ ] Code with Claude Tokyo Conference page で speaker submission form 確認
- [ ] Side event 場所 candidate 3つ list
- [ ] Side event 日時決定 (6/9 vs 6/10)
- [ ] X "Tokyo conf 行きます" pre-thread 投下
- [ ] Tokyo 在住の Linksee Memory user / Synapse Arrows fan を探す
