# Tokyo Conference 6/10 — Strategy (Virtual-only era)

> Status: 策定中、 2026-05-07 起案 → **5/7 PM 大幅修正** (virtual-only 判明)
> Conference: Code with Claude — Tokyo, 2026-06-10 **(VIRTUAL ONLY)**
> Days remaining: ~34 days (5/7 → 6/10)
> Owner: Michie (戦略) + Cofounder Claude (物量 / online content)
> Companions: [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md), [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md)

## 🔴 2026-05-07 PM 重要更新: Conference は **virtual のみ**

Michie 確認 (5/7): 物理参加の募集はすでに終了、 **virtual 視聴のみ** が残された参加形式。 strategy 全面見直し。

### Virtual-only であることの structural impact

| 当初想定 (物理) | 実情 (virtual) |
|---|---|
| Boris Cherny / Ami Vora と直接 face-to-face | online のみ、 chat / Q&A 経由 |
| 名刺交換 / hallway track | X / LinkedIn DM が main |
| Side event 主催で参加者集約 | 物理参加者がいない、 audience 構造変化 |
| Demo を物理 booth で見せる | online で配信 / 動画 / X 経由 |
| Networking で anchor customer 発掘 | online 経由のみ、 conversion 弱め |

→ **「conference 物理参加 ride-along」という戦略は無効化**。

### では Synapse Arrows にとって 6/10 はまだ価値があるのか?

**Yes、 むしろ違う形で価値が高まる可能性**:

1. **virtual 参加者は SNS にいる** — X / LinkedIn / Discord で全員到達可能
2. **物理 friction 解消** — Anthropic eng の attention は会場ではなく、 配信 + reaction tweet に分散
3. **コスト 0** — Tokyo 出張不要、 余った budget / 時間を online content に投下
4. **同時視聴の "online community moment"** — X 上で realtime 反応大会、 Synapse Arrows がそこにいるかどうか

→ **「Tokyo Conference 6/10 を Synapse Arrows brand の major launch moment として使う、 ただし online 主戦場で」** が新 strategy。

## Why this conference still matters (revised)

Anthropic 主催の Tokyo conference はおそらく 2026 年で **アジア最大の Claude / MCP イベント** (= **online でも attention 集中する moment**)。
Boris Cherny / Ami Vora / Angela Jiang クラスが登壇 (= **virtual 視聴経由でも、 配信中の reaction が彼らに届く可能性**)。

Synapse Arrows にとって:

1. **Linksee Memory Pro tier launch のタイミング** (online で「同日 launch」narrative が effective)
2. **KanseiLink Cockpit Web UI の online demo first impression** (動画で再利用可能)
3. **Anthropic eng への online reach** (X engagement / live tweet stream)
4. **日本 dev / 税理士コミュニティの online 集積タイミング**

## Reality check — 公式 talk 枠は厳しい

### 通常の Anthropic conference の speaker 確定 timing

Code with Claude 系イベントの speaker lineup は通常 **2-3か月前 lock**。 5/7 時点で 6/10 conference には残り 34日 = ほぼ確実に主要枠は closed。 Virtual-only でも同じ。

### 残された4 path

| Path | 確率 | 効果 | 工数 | Owner |
|---|---|---|---|---|
| **A. 公式 talk submission** | 5-10% | 高 (登壇者として brand) | 小 (申請のみ) | Michie + Cofounder |
| **B. Lightning talk / sponsor 枠 申請** | 15-25% (有料) | 中 | 小 | Michie |
| **C. Demo / community slot 申請** | 30-40% | 中 | 小 | Michie |
| **D. Side event 主催** (前夜 or after) | **70%** (自分で動ける) | 中〜高 | 中 | Michie + Cofounder |

→ **D を main、 A-C は parallel に申請** が現実解。

## Path D — Side event 主催 (主戦略)

### Concept (revised: Online Demo Day)

```
タイトル: "Synapse Arrows Demo Day — MCP Cockpit Showcase"
副題: "5 MCP blocks 全実装事例 / 日本会計 AI cockpit / Solo founder の OS architecture"
日時: 6月10日 (火) 22:00-23:30 JST (Conference 終了直後)
       or 6月11日 (水) 12:00-13:30 JST (lunch time)
形式: YouTube Live + X Spaces (二画面)
        Live demo + slide + Q&A
規模: 50-200人 (online、 録画は永続)
費用: ¥0 (純 online、 OBS Studio + zoom 等)
募集: X / Zenn / Conference 視聴者 hashtag 経由
録画: 永続 asset 化、 後日 Zenn 第3弾 + Dev.to に embed
```

### Agenda (90 min online program)

```
22:00-22:05  Opening (Michie)
              "今日 Tokyo Conference 視聴お疲れ様でした、
               私たちの番です"
22:05-22:20  Synapse Arrows 全体 pitch (Michie)
              "Solo founder + 5 product + Self-similar OS architecture"
22:20-22:40  Linksee Memory v0.3 demo (live screen share)
              "5 MCP blocks 全実装事例 — 業界初"
              実 demo: Resources / Sampling / Server-side Agent Loop /
                       Elicitation / Roots
              waitlist signup link 配布
22:40-23:00  **KanseiLink Cockpit demo** (Web UI live walk-through)
              "顧客データ流出させずに Japan 会計を AI 自動化"
              実 demo: Web cockpit dashboard 上で
                1 click → TDnet 開示 → freee 仕訳 candidate → audit log
              "親世代の税理士でも使える" UI を見せる
              pilot 申込 form 配布
23:00-23:15  Q&A (X Spaces / YouTube chat)
              Anthropic eng / dev community からの質問拾う
23:15-23:30  Synapse Arrows Playbook 紹介 + 次の動き
              "Public OSS doc / Series A までの roadmap"
              follow / star / waitlist の3つの ask 明示
```

### Why this works (online era)

- **Conference attention の余熱を捕まえる**: 視聴後22時帯は「もう少し関連 content 見たい」mode
- **録画が永続 asset**: Zenn 第3弾 / Dev.to 英語版に embed、 半年売れる
- **Global reach**: Tokyo 物理 50人 → online 200-500人 + 動画再生千数千
- **コスト 0**: Tokyo 出張費 / 会場費が浮く分を online 配信質に投下
- **Anthropic eng が反応しやすい**: Tweet で mention すれば届く可能性高い (会場で名刺交換より easy)

### 実施リスク (online 版)

| Risk | Mitigation |
|---|---|
| 集客失敗 (10人未満視聴) | X thread 連投 + Zenn 第2弾末尾に告知 + Conference hashtag に live tweet |
| 配信トラブル | リハーサル 1回 (前日)、 backup として Zoom recording |
| Anthropic との時間被り (まだ session 中) | 22:00 JST 開始 = Tokyo conf 終了予定後 |
| 日本語 only / 英語 only どちら | bilingual: presenter は日本語、 slide / 字幕 英語 |
| 録画 quality 低い | OBS Studio + 1080p + good mic + 静かな部屋 |

## Path F — Conference 同時 live tweet stream (low effort, high return)

会場物理にいない = 邪魔されず X 反応大会できる立場。

### Strategy

```
6/10 当日 09:00-18:00:
  ・Conference 視聴 (virtual)
  ・X で keynote ごとに reaction tweet
  ・各 talk の key insight を 280 字で要約 + 自分の解釈
  ・Synapse Arrows 関連性のある内容で thread 化
  ・hashtag #CodeWithClaude / #ClaudeCodeTokyo に乗る

例: "Boris just said X. This is exactly what we shipped in
     Linksee Memory v0.3 last week. → [link]"

20:00-22:00:
  ・1日の summary thread 投下
  ・"明日 Demo Day で詳しく話します" link

22:00-23:30:
  ・Path E の Online Demo Day を実施
```

### Why this works

- **会場のロジスティクスから完全独立** = 落ち着いて深い content 出せる
- **Conference 公式 hashtag 経由で attention 流入**
- **Anthropic eng が反応する可能性高い** (live で thoughtful tweet 出していると noticed されやすい)
- **後日 Zenn 第3弾の素材**: 「Code with Claude Tokyo 2026 で見えた MCP の未来」

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

→ 現状 (bootstrap) は **pass + Path E (Online Demo Day) 集中** が妥当。 funding / pilot revenue 入った段階で次回検討。

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

### Slide 構成 (12-15 slides) — Online Demo Day 用

```
1. Title: "Synapse Arrows — A Solo Founder's MCP-Native OS"
   subtitle: "5 products, 1 operating system, public playbook"
2. The story: 4か月前まで普通の Solo dev 問題 → 5 product OS
3. Linksee Memory: local-first 6-layer memory (1,903 DL)
4. KanseiLink: Japanese SaaS intelligence (200+ catalog)
5. KanseiLink Cockpit (NEW): Web UI for tax accountants
6. ScaNavi: vertical sake recommendation
7. CardWize: vertical credit card optimization
8. ReviewLens: vertical cosmetics review
9. The OS: Synapse Arrows Playbook (public)
   "Same OS at every scale: company → product → embedded agent → user"
10. Today's milestone: Linksee Memory v0.3 = 5 MCP blocks 全実装
11. Today's pivot: KanseiLink Cockpit = Anthropic 補完 + Japan security narrative
12. The 12-month plan: $10K MRR (bootstrap) → $100K → ?
13. Why now: Tokyo Conference 2026 が分水嶺
14. Ask: waitlist signup / pilot customer / dev contributors
15. Contact: Michie / synapsearrows.com / linksee.com / kansei-link.com
```

### 1-pager handout (online 配布用 PDF)

A4 1枚、両面:

```
Front:
  Synapse Arrows — Singapore-based, MCP-native, 5 products, public Playbook
  Logo + 5 product overview + traction numbers
  QR: synapsearrows.com

Back:
  Linksee Memory: 1,903 DL / 5 blocks 実装 / Pro tier $5/mo
  KanseiLink Cockpit: 税理士向け AI 操縦席 / pilot ¥30K/mo
  Online Demo Day: 6/10 22:00 JST (YouTube Live + X Spaces)
  Contact: Michie Yamaguchi / @ELLECraftsinga1
```

→ Online 配布: linksee.com に download link、 X thread に embed、 Zenn 末尾 CTA

### 名刺 (英文) — virtual era では QR ベース

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

- **X で「6/10 Online Demo Day 開催」 thread 投下** (Tokyo Conf 同日 22:00 JST)
- Anthropic Tokyo team に follow + DM (online で reach、 物理会わない前提)
- Boris Cherny / Ami Vora / Angela Jiang に X follow + 軽い engagement
- punkpeye (Glama) に「Conference 視聴中? Demo Day 来てください」 DM
- Composio 日本担当 (もしいれば) reach
- 既存 Linksee Memory user 全員 invite (online なので地域制約なし)
- **freee/MF 使う税理士で SNS 発信している人を 10-20人 follow + DM** (KanseiLink Cockpit pilot 候補)
- **会計士・税理士コミュニティ (X / Note / 業界 Slack) に Demo Day 投下**
  → 税理士は engineer 系 conference に来ない、 online Demo Day なら参加可能
- **MCP Discord、 Anthropic developer Discord に Demo Day 告知**

### Conference day (virtual viewing)

- 09:00-18:00: Conference 視聴 + live tweet (Path F)
- 各 talk ごとに reaction tweet
- key quote の screenshot + Synapse Arrows 関連性 thread 化
- conference hashtag に乗る

### Online Demo Day (6/10 22:00 JST)

- OBS Studio + 1080p camera + good mic 準備
- Linksee Memory v0.3 demo (live screen share)
- KanseiLink Cockpit Web UI demo (live walk-through)
- TDnet 開示 sample データ準備
- YouTube Live + X Spaces 同時配信
- 録画 → Zenn 第3弾 / Dev.to 英語版 embed

### Post-conference follow-up routine

```
Day 0 (6/10 conference 当日):
  09-18:  live tweet stream (Path F)
  20-22:  1日 summary thread + Demo Day 告知再投下
  22-23:30: Online Demo Day live (Path E)
  23:30:   Demo Day 録画即 upload (YouTube)、 X thread で告知

Day 1 (6/11):
  Demo Day 視聴者全員に個別 thanks DM
  深く engaged だった人 5-10人に long-form DM:
    "デモした Linksee Memory / KanseiLink Cockpit について追加情報"
  Demo 録画を Linksee.com / Synapse Arrows website に embed

Day 7 (6/17):
  pilot 候補 (会計事務所 etc) に formal proposal メール
  Linksee Memory waitlist signup → Pro tier conversion 動向確認

Day 14 (6/24):
  Conference + Demo Day 振り返り Zenn 第3弾 公開
  "Code with Claude Tokyo で見えた MCP の未来 + 私たちが launched したもの"
  Demo 録画 embed、 X thread 連動
  Dev.to 英語版同時公開
```

## Pre-Tokyo Sprint (5月W2-W4 + 6月W1)

Online Demo Day 6/10 までに揃えたいもの (4 weeks):

```
Week 1 (5/12-5/18):
  - Linksee Memory Resources 実装
  - KanseiLink Cockpit Web UI wireframe
  - Online Demo Day 日時確定 (6/10 22:00 JST 推奨)

Week 2 (5/19-5/25):
  - Linksee Memory Sampling + Server-side Agent Loop
  - KanseiLink Cockpit Web UI Workflow 1 (J-GAAP) 実装
  - Pitch deck v1 / 1-pager PDF / online 自己紹介素材
  - OBS Studio セットアップ + 配信リハーサル

Week 3 (5/26-6/1):
  - Linksee Memory Elicitation + 日英 bilingual
  - KanseiLink Cockpit demo flow 完成
  - Online Demo Day 募集開始 (X / Zenn 第2弾末尾 / Discord)
  - Anthropic Tokyo team 個別 X reach

Week 4 (6/2-6/8):
  - Linksee Memory Pro tier landing page launch
  - Stripe 接続 + 30日 trial 設定
  - Synapse Arrows Playbook v0.3.x 全公開
  - Online Demo Day 配信リハーサル (前日 6/9)

Day 0 (6/10):
  - 09-18 conference live tweet
  - 22-23:30 Online Demo Day live 配信
  - 録画即 upload
```

## Success metrics (Tokyo Conference 期間 — virtual era)

| KPI | Min target | Stretch |
|---|---|---|
| Online Demo Day live 視聴者 | 50人 | 200人 |
| Demo 録画 7日間視聴 | 200回 | 1000回 |
| Linksee Memory waitlist signup (Tokyo Conf 由来) | 50人 | 200人 |
| **KanseiLink Cockpit pilot interest** 取得 | **1社** | **5社** |
| Anthropic eng X engagement (RT/reply) | 1件 | 5件 |
| Press / blog mention | 0 | 1-2本 |
| Synapse Arrows Playbook GitHub stars | +20 | +100 |
| **税理士・会計士 contact 取得** | **5人** | **20人** |
| Conference live tweet impressions | 10K | 100K |
| Demo Day 後の new X follower | +50 | +200 |

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
