# KanseiLink — Finance Vertical Pivot (Layered Strategy)

> Status: strategic pivot, 2026-05-07 起案
> Owner: Michie (B2B sales) + Cofounder Claude (strategy)
> Predecessors: 既存 KanseiLink MCP intelligence layer (200+ Japanese SaaS catalog)
> Companions: [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md), [06-tokyo-conference-strategy](./06-tokyo-conference-strategy.md)

## Why pivot now

### 2026-05-07 時点の状況

- KanseiLink は元々 「日本 SaaS の MCP intelligence layer」 として構築 (≈ Composio Japan 版)
- 200+ Japanese + Global SaaS を index 済
- MCP tools (search, recipe, audit_cost, agent_voice 等) 実装済
- **B2B paying customer 0** (現状 free public access)
- Composio が $29M raise で global 進出加速、 Japan 進出は時間の問題

### 二つの pressure

1. **Composio の Japan 進出 (時間問題)**
   - Composio: 100K developer + 200 enterprise + 7-figure revenue
   - Japan に来た瞬間、generic "Japan SaaS catalog" だけで戦うのは厳しい

2. **Anthropic 自身が finance vertical に来た**
   - 2026-04-08: Claude Managed Agents launch
   - Microsoft 365 integration (Excel / PowerPoint / Outlook / Word)
   - **Finance ready-to-run agents 10種類 + Moody's MCP app**
   - Pitch builder / Meeting preparer / Earnings reviewer / Model builder / Market researcher / Valuation reviewer / GL reconciler / Month-end closer / Statement auditor / KYC

→ **「Generic Japanese SaaS catalog」 では遅い、 「Anthropic finance tools の Japan ブリッジ」 で先行する**。

### 鍵となる外部 insight (2026-05-07 X 投稿)

> 「金融業界や投資業界の一番のネックはセキュリティー問題なので、AnthropicのAI スタートアップがたくさんのツールを出してきているけれど、法人系に使われるようになるのには別なハードルがある [...] 個人レベルで [...] かなり強い」

→ **enterprise security 問題で大手 / 上場企業の本格導入はブロック**、 **個人 / 中小事務所 / SMB 経理担当はすでに使い始めている**。market gap が一時的に開いている。

## Strategic positioning (二層構造)

### Layer 1 (基盤): Japanese Composio 

200+ Japanese SaaS catalog + MCP intelligence + recipe / agent_voice / audit_cost。
**変えない**。これが kanselink.com の実体。

### Layer 2 (拡張): Finance / Accounting Vertical

Layer 1 の上に **特化 product** を3つ build:
1. **J-GAAP Earnings Reviewer** — TDnet / EDINET 資料 → freee 連携 → AI summary
2. **Month-end Closer for 会計事務所** — 弥生 / freee の月次決算 AI 自動化
3. **Statement Auditor for 経費精算** — freee 経費 → 異常検知 + 異議メモ

これらは **Anthropic の global tools の Japan ブリッジ** として positioning。

### なぜこれが刺さるか — 3つの構造的理由

#### 理由1: Anthropic が cover していない gap

Anthropic finance tools は global 共通仕様:
- US-GAAP / IFRS 中心、 J-GAAP 未対応
- SEC 開示形式、 TDnet / EDINET 未対応
- QuickBooks / Xero 連携、 freee / Money Forward / 弥生 未対応
- USD / EUR ベース、 JPY 特殊扱い (消費税 / 源泉徴収 / 法人税) 未対応

→ **KanseiLink がこの gap を埋める** = Anthropic と競合せず補完。Stripe (global) + GMO ペパボ (Japan) と同じ関係性。

#### 理由2: 既存資産との完全 fit

KanseiLink が既に持っているもの:

| 資産 | 金融 vertical での活用 |
|---|---|
| freee 連携 recipe | Earnings reviewer / Month-end closer の core 部品 |
| Money Forward 連携 recipe | 同上 |
| 弥生 / TKC catalog | 会計事務所 ICP 向け SaaS bridge |
| audit_cost tool | Statement auditor の前身 |
| agent_voice | finance professional 経験 voice 集め |
| MCP intelligence layer | 全部 MCP server として統合可能 |

→ **8割揃っている**。残り20% = vertical specific feature + sales motion。

#### 理由3: Solo founder fit が高い

| 比較軸 | Generic "Japanese Composio" | Finance vertical |
|---|---|---|
| ICP 明確度 | 不明 (誰が払う?) | **明確 (会計事務所 / 個人 CFA / 中小経理)** |
| Sales cycle | enterprise 12-18か月 | **中小 1-3か月** |
| 競合 | Composio (時間問題) | **Anthropic 補完** (競合せず) |
| Founder fit | 一般 | **Bilingual + Japan + 戦略 = perfect fit** |
| 解約リスク | 高 (commodity) | **低 (workflow 統合度高)** |

## Target ICP (3層)

### ICP-A: 会計事務所 (1-30人規模)

**Pain**:
- 月次決算で同じ作業を毎月繰り返す
- 顧客企業 50-200社の経理データを横断
- freee / Money Forward / 弥生 を顧客毎に切替え
- 月末の閉め作業が一週間集中

**Linksee Memory + KanseiLink の value**:
- 月次 close routine の AI 自動化
- 顧客 × 過去 N か月の異常検知
- 「いつもと違う仕訳」 alert
- **value prop**: 「月次決算が3日 → 1日に」

**価格 hypothesis**: ¥30,000 / 月 / 事務所
**Sales motion**: 既存知人 / 紹介 / 会計事務所コミュニティ

### ICP-B: 個人 CFA / 投資銀行アナリスト / 個人投資家

**Pain**:
- TDnet / EDINET 大量資料を読む必要
- Excel で財務モデル毎回ゼロから
- 競合ベンチマーク調査が労働集約

**Value**:
- 開示資料 → 財務モデル自動生成
- 業界ベンチマーク 比較 (200+ SaaS 横断)
- Microsoft 365 連携 (Excel → PPT → Outlook flow)

**価格 hypothesis**: ¥10,000 / 月 / 個人
**Sales motion**: X / Note 個人発信 + financial vertical community

### ICP-C: 中小企業 経理担当 (50-300人規模)

**Pain**:
- freee / 弥生 の使いこなし足りない
- 経費精算の異常検知 (不正 or 入力ミス)
- 月次レポート作成

**Value**:
- 経費自動 audit
- 月次 close 半自動化
- AI assistant 搭載 ("freee の使い方教えて")

**価格 hypothesis**: ¥50,000-100,000 / 月 / 企業
**Sales motion**: SMB outbound + 紹介

## Product roadmap (3 specific products)

### Product 1: J-GAAP Earnings Reviewer (Tokyo Conf 6/10 までに demo)

**Description**:
TDnet 開示資料 (PDF / XBRL) を読み込み → AI が financial summary 生成 → freee と突合 → 異常検知。

**Tech stack**:
- TDnet RSS feed monitor
- XBRL parser
- Claude (Sampling 経由) で summary
- freee API (既存 KanseiLink recipe)

**Demo target**:
"上場企業の決算開示が出た瞬間に、 freee に登録された自社情報と突合して、AI が 30秒で財務 summary を生成する"

### Product 2: Month-end Closer for 会計事務所 (6月-7月)

**Description**:
顧客企業の月次決算 routine を AI が自動化。仕訳チェック → 月次レポート → 顧客報告メール下書き。

**Tech stack**:
- 弥生 / freee / Money Forward API integration
- Claude Sampling で 仕訳判定
- Microsoft 365 Outlook integration (メール下書き)
- Linksee Memory で 顧客 × 過去判断 を記憶

**Sales target**:
3-5 会計事務所が pilot (¥30K/mo × 5 = ¥150K MRR)

### Product 3: Statement Auditor for 経費精算 (7月-8月)

**Description**:
freee 経費データを毎日 monitor → 異常検知 (金額 / カテゴリ / 頻度) → AI が "確認すべき経費" レポート生成。

**Tech stack**:
- freee API (既存)
- KanseiLink reconnaissance ant pattern を流用
- Linksee Memory で会社固有の "正常パターン" 学習

**Sales target**:
中小企業経理 5-10社 (¥50K/mo × 5 = ¥250K MRR)

## 6か月後 (2026-11) の想定 state

| 指標 | 現状 (5/7) | 6か月後 target |
|---|---|---|
| KanseiLink B2B paying customers | 0 | 10-20 |
| MRR | $0 | $5-10K (= ¥75K-150万 月商) |
| ICP-A (会計事務所) pilot | 0 | 5社 |
| ICP-B (個人 finance pro) | 0 | 50人 |
| ICP-C (中小企業) | 0 | 5社 |
| ARR | $0 | $60-120K |

**月 $10K MRR 達成 = bootstrap "勝ち" 第一段階**。

## Sales motion plan

### Phase 1 (5月-6月): Tokyo Conference 中心の早期 anchor 取り

- Tokyo Conference 6/10 で 5-10社 contact
- 1社が pilot に乗ったら anchor → case study 化
- pilot 中の friction 全部 product 改善 input

### Phase 2 (7月-8月): 紹介経由の expand

- pilot 1社が working → 同業 (会計事務所コミュニティ) で口コミ
- ICP-A 会計事務所 5社 reach 目標
- ICP-B 個人 finance professional は X / Note で個人発信

### Phase 3 (9月-): SMB outbound

- ICP-C 中小企業を targeted outbound
- 月 $10K MRR 達成検証

## 既存資産との接続性 map

```
[現 KanseiLink]
  ├── search_services tool        → Layer 2 product 全部で活用
  ├── get_recipe tool              → freee/弥生 連携 recipe を vertical 用に拡張
  ├── audit_cost tool              → Statement Auditor の前身、 finance 向け再設計
  ├── agent_voice tool             → finance professional voice 収集に転用
  ├── reconnaissance ant           → Statement Auditor の monitoring 部分に流用
  └── KanseiLink web dashboard     → ICP-B 個人 finance professional 向け web UI

[新 finance vertical features]
  ├── J-GAAP Earnings Reviewer     ← TDnet/EDINET parser 新規
  ├── Month-end Closer             ← Microsoft 365 連携新規
  └── Statement Auditor            ← reconnaissance ant 流用
```

## Risk & mitigation

| Risk | Mitigation |
|---|---|
| Composio が Japan 進出して generic 領域で attack | finance vertical 先行 = 競合せず差別化 (Stripe vs GMO の関係) |
| Anthropic 自身が J-GAAP 対応 | unlikely (vertical 特殊性高すぎ)、 仮に来ても KanseiLink は SMB 向け |
| 会計事務所 sales cycle が長い | pilot 価格 ¥0-10K で friction ゼロにする |
| 単一 founder で営業 capacity 限界 | Cofounder Claude が pre-sales / RFP / proposal 自動化 |
| 金融 vertical 特化で "general MCP" brand 失う | Layer 1 (Japanese Composio) を維持、Layer 2 が "first product" |

## DECISIONS log

### 2026-05-07 — Finance Vertical Pivot 決定

**CONTEXT**:
KanseiLink が generic "Japanese Composio" として2 か月運営後、 paying customer 0 のまま。 Composio $29M war chest + Anthropic finance vertical 進出で、 generic では遠からず squeezed される。

X 投稿 (2026-05-07) で「金融 vertical の SMB / 個人レベルは market gap 開いている」と判明。 既存 KanseiLink 資産 (freee/弥生 recipe / audit_cost / agent_voice) が finance vertical に 80% fit する。

**DECISION**:
- KanseiLink を二層構造化:
  - Layer 1 (基盤): Japanese Composio (catalog + intelligence) **変更なし**
  - Layer 2 (拡張): Finance Vertical specialization
- Tokyo Conference 6/10 までに **J-GAAP Earnings Reviewer** demo
- 6か月で月 $10K MRR target (10-20 paying customers)

**REASON**:
1. **既存資産 fit 80%** → 新規 build コスト最小
2. **Anthropic 補完** = 競合せず売れる
3. **SMB 個人 ICP** = security barrier 回避、 sales cycle 短い
4. **Solo founder fit** = Michie の bilingual + 戦略 + Japan が完璧 fit

**REVERSIBILITY**:
Medium — Layer 2 product を撤退すれば Layer 1 (Composio Japan 版) に戻れる
ただし Tokyo Conference で finance positioning を発信した後の方向転換は brand コスト

**OPEN QUESTIONS**:
- 第一 anchor customer は会計事務所か中小企業か個人か?
- 価格点 ¥30K / ¥50K / ¥100K のどこが SMB sweet spot か?
- Microsoft 365 統合は self-build か Anthropic Add-in 経由か?
- finance professional コミュニティ (会計士会 / CFA Japan / Note finance writer) との接続経路は?

## Linked Synapse Arrows assets

- Existing KanseiLink: https://kansei-link.com / repo `kansei-link-mcp`
- Reconnaissance ant (運用 cofounder Claude が今日構築済): `scripts/reconnaissance/`
- HEALTH.json + scope-locks pattern (process)
- Linksee Memory との連携 (entity-based memory が finance professional 個別 workflow を覚える)

## Anti-patterns to avoid

- **「Anthropic と全面戦争」 positioning** → 補完で売る、競合と書かない
- **enterprise からアプローチ** → SMB / 個人で実証してから enterprise
- **会計法律 compliance を pre-emptively 全部対応** → minimum viable で出して fix
- **sales を全部 founder が** → cofounder Claude を pre-sales / RFP 起草で活用
- **Layer 1 (基盤) を捨てる** → Layer 1 が moat、 Layer 2 はそれの上の差別化

## Next actions (this week)

- [ ] 5/12 までに ICP-A (会計事務所) の network 5社 list up
- [ ] 5/12 までに J-GAAP Earnings Reviewer の demo scope decided
- [ ] 5/19 までに Tokyo conf 用 KanseiLink 1-pager 草案
- [ ] 5/26 までに pilot 価格 / 契約 template
- [ ] 6/8 までに demo 動作確認

## Companion docs

- 同 sprint で Linksee Memory Pro tier も launch (4-week sprint): [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md)
- Tokyo Conference での露出 strategy: [06-tokyo-conference-strategy](./06-tokyo-conference-strategy.md)
