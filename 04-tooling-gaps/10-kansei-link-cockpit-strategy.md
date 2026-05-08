# KanseiLink Cockpit — Strategy Manifesto

> Status: 確立、 2026-05-08 (戦略 crystallization 完了)
> Owner: Michie (技術スタック作り込み) + Cofounder Claude (strategy / draft / API design)
> Marketing partners: Hatakeyama Kento + 税理士 info-product cluster (= 共同体 evangelism)
> Companions: [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md), [07-kansei-link-cockpit-security-posture](./07-kansei-link-cockpit-security-posture.md), [09-zenn-pain-first-playbook](./09-zenn-pain-first-playbook.md)

## Table of Contents

1. [Why Cockpit (= MCP 経済の monetization 課題)](#1-why-cockpit)
2. [3-Layer Model](#2-3-layer-model)
3. [Notion unbundle narrative](#3-notion-unbundle)
4. [Cockpit = Dashboard Generation Engine (= 上位概念)](#4-dashboard-generation-engine)
5. [5 つの core 機能](#5-5-つの-core-機能)
6. [Pricing thesis: Free MCP / Paid Dashboard](#6-pricing-thesis)
7. [Year 1 (product) / Year 2 (platform marketplace)](#7-year-1-2-phase)
8. [Synapse Arrows OS との 一貫性](#8-os-一貫性)
9. [競合 landscape (2026-05 時点)](#9-競合-landscape)
10. [MVP scope (5/31 pilot 1 firm)](#10-mvp-scope)
11. [Hatakeyama partnership pitch](#11-hatakeyama-pitch)
12. [Marketplace 経済学 (Year 2)](#12-marketplace-経済学)
13. [Risks + mitigation](#13-risks)

---

## 1. Why Cockpit

### 課題: MCP / AI app builders は今稼げていない

2026-05 時点の事実:
- MCP server を OSS で配っても、 単体では monetization 困難
- AI plugin / Custom GPT を作っても、 Anthropic / OpenAI marketplace の収益還元は薄い
- 独立 MCP dev は consulting に頼るしかなく、 それは時間切売り = scale しない

→ MCP / AI 時代の builders は **「技術はあるが場が無い」** 状態。

### 同時に: 各 vertical の業務担当者は AI を使いたいが skill が足りない

- 税理士は 「Claude × freee 自動化」 をしたいが、 Claude Code / MCP / CLAUDE.md / skill 化 を自分では組めない
- 法律事務所、 医院、 不動産、 建設、 etc. — どの vertical も同じ pain
- Hatakeyama Kento (公認会計士) は例外的に 6 ヶ月で構築できたが、 99.9% の同業者は不可能

### Cockpit = 両者の中間に立つ場

- **建てる側 (= MCP / AI builders)**: technical skill を生かして dashboard を設計、 顧客に売る、 Cockpit は 30% margin で revenue share
- **使う側 (= vertical 業務担当者)**: pre-built dashboard を 5 分で導入、 ¥30K-200K/月 を払う
- **Cockpit (= 我々)**: 場を提供、 vertical-first で start、 marketplace 化で scale

これは **MCP 経済の 2026 段階で必要な monetization layer** = 業界全体への貢献でもある。

---

## 2. 3-Layer Model

```
┌─────────────────────────────────────────────────────────────┐
│ Layer 3: Collaboration / Customer Dashboard                  │
│ ─ team 共有 view (= 税理士法人内 5-10 人で見る)              │ ← Cockpit の戦場
│ ─ 顧問先 view (= 顧客の経営者・経理担当が見る)               │
│ ─ レポート / 通知 / アーカイブ / 共有 / 削除証明書             │
├─────────────────────────────────────────────────────────────┤
│ Layer 2: Personal Workspace (= 個人 AI UI)                    │
│ ─ Claude / GPT / Cursor / Codex / Gemini CLI                 │
│ ─ Skill / Routine / Schedule / @-mention                     │
│ ─ 税理士 1 人が AI と対話する作業台                           │
├─────────────────────────────────────────────────────────────┤
│ Layer 1: Execution Engine                                     │
│ ─ Anthropic Finance Agents (Month-end closer / GL reconciler)│
│ ─ Claude Skills / Anthropic Apps                             │
│ ─ OpenAI Apps / Custom GPTs                                   │
│ ─ MCP servers (freee / MF / Sansan / Gmail / KanseiLink ...)│
└─────────────────────────────────────────────────────────────┘
```

### 各 Layer の play 比較

| Layer | Anthropic | freee/MF | Notion | **Cockpit** |
|---|---|---|---|---|
| L1 Engine | 🟢 own | 🟡 connector | 🟡 (Notion AI) | ❌ ride (rent) |
| L2 Workspace | 🟢 own (Claude) | ❌ | 🟢 own | ❌ ride (rent) |
| L3 Collaboration | ❌ (Claude は個人 UI) | 🟡 (顧問先 view 弱い) | 🟡 (汎用) | 🟢 **取りに行く** |

→ Anthropic / OpenAI は L1+L2 で勝負、 Cockpit は L3 で勝負。 互いの戦場が違う = head-on にならない、 補完関係。

---

## 3. Notion unbundle narrative

Notion は **5 layer 全部 1 bundle で seat 課金**:

```
┌────────────────────────────────────┐
│  Notion bundle (1 つの料金)         │
├────────────────────────────────────┤
│ 5. Sharing / Collaboration         │
│ 4. Dashboard / Templates           │
│ 3. AI Execution                    │ ← Notion AI
│ 2. Workspace                       │ ← Notion editor
│ 1. Data Storage                    │ ← Notion DB
└────────────────────────────────────┘
```

Cockpit は これを **unbundle**:

```
┌──────────────────────────────────────────────┐
│  Cockpit                                       │
├──────────────────────────────────────────────┤
│ 5. Sharing / Collaboration   ← ✅ ここで課金   │
│ 4. Dashboard / Templates     ← ✅ ここで課金   │
├──────────────────────────────────────────────┤
│ 3. AI Execution      ← Anthropic に rent     │
│ 2. Workspace         ← Claude/GPT に rent    │
│ 1. Data Storage      ← freee/MF に rent      │
└──────────────────────────────────────────────┘
```

### LP / pitch 用 1 文 narrative

> **「税理士・会計事務所のための Notion。 ただし AI と data は外注、 dashboard と共有層だけ最適化した。」**

または:

> **「Linear が GitHub を借りるように、 Cockpit は Claude を借りる。 dashboard と共有だけ作り込む。」**

---

## 4. Dashboard Generation Engine

Cockpit は単なる「税理士向け固定 dashboard」 ではなく、 **動的に dashboard を生成する engine**:

```
入力 (= 個人の context)
├ 役割: 税理士 / スタッフ / 顧問先
├ 時間: 朝 / 月末 / 決算期
├ 目的: 月次決算 / 商談準備 / 確定申告
└ 接続済 SaaS: freee / MF / Notion / Slack / Gmail / Cal

       ↓ AI が選ぶ + 組成

Cockpit Dashboard (= 即座に最適化された 1 view)
├ 必要な data だけ pull (= 過剰情報なし)
├ 必要な action button だけ表示 (= cognitive load 最小)
├ 裏で最適 LLM が動く (Claude / GPT / Codex / Gemini)
└ Skill 選択 / token 最適化 / prompt engineering 全自動
```

→ **「ダッシュボードの鬼」** = 1 個 1 個の dashboard を ridiculously に最適化する brand promise。

---

## 5. 5 つの core 機能

### 機能 1: 🧱 Dashboard Pattern Library
- ScaNavi が何百もの sake DB を構造化したように、 Cockpit も **何百もの dashboard pattern** を構造化
- 「月次決算進捗 view」 / 「顧問先打合せ準備 view」 / 「異常仕訳レビュー view」 / 「年末調整進捗 view」 / ...
- 各 pattern が **AI が参照可能な metadata** を持つ
- = 競合が複製困難な時間積立 (= moat)

### 機能 2: 🔀 LLM Agnostic Routing
- ユーザーは LLM を選ばない
- Cockpit が task 性質で **最適 LLM を裏で選ぶ**:
  - 仕訳判定 → Claude (long context / reasoning)
  - 簡単分類 → GPT-5 mini (cheap / fast)
  - コード生成 → Codex
  - 日本語要約 → Gemini Flash (CJK)
- KanseiLink の AEO ranking + audit_cost が routing engine の foundation

### 機能 3: 🔗 Multi-Source MCP Integration
- 独自 MCP (Hatakeyama-style Cockpit MCP)
- Linksee Memory like MCP (個人 context 永続記憶)
- Cross-connect MCP (freee ↔ MF reconciliation engine、 Cockpit 独自)
- 200+ Japanese SaaS の MCP (KanseiLink catalog 流用)
- → ユーザー視点では 「全部入ってる単一 dashboard」

### 機能 4: 🧠 Personal Context Awareness
- 田中税理士 朝 9:00 = 月次決算 dashboard
- 田中税理士 午後 = 顧問先打合せ準備 dashboard
- スタッフ A = 担当 5 社 view
- 顧問先 = 自分の会社 status only
- → Linksee Memory が個人 context (goal / context / emotion / caveat) を保持、 Cockpit がそれを参照
- → **「生きてる view」** (= 静的 dashboard ではない)

### 機能 5: 🎯 Vertical Deep Specialization
- Year 1 = 税理士 vertical 鬼レベル特化で start
- 税理士業界 dominance 確立後、 法律事務所 / 医院 / 工務店 等に展開
- 各 vertical で 「ダッシュボードの鬼」 position を取る

---

## 6. Pricing thesis

### 基本: Free MCP / Paid Dashboard

| 部分 | 価格 | 理由 |
|---|---|---|
| MCP / Skill / Preset 配布 | **Free (OSS / npm / Anthropic Plugin)** | adoption friction 0、 lead funnel |
| Dashboard / Sharing / Team / Customer view | **Paid** | ここでしか課金しない |

→ Notion 反転戦略。 Adoption は無料、 monetization は dashboard layer のみ。

### Tier 設計 (= MVP 想定)

| Tier | 月額 | 何が解放 |
|---|---|---|
| **Free** | ¥0 | OSS MCP + Skill + Preset (= solo 税理士の DIY 路線そのまま) |
| **Solo Pro** | ¥10,000 | 個人 dashboard (60 顧問先 grid) + 月次レポート + AI 通知 |
| **Team** | ¥30,000-50,000 | 上記 + チーム共同編集 + 担当 assign + 異常 alert + audit log |
| **Customer-facing** | ¥80,000-150,000 | 上記 + 顧問先 view + DPA + 削除証明書 + Phase 1 Security |
| **Enterprise** | ¥200,000+ | 上記 + SSO / on-premise / SLA / 専任サポート |

### Linksee Memory との一貫性

| 製品 | Free | Paid |
|---|---|---|
| Linksee Memory | OSS local-first MCP | Pro tier (cross-device sync / team shared memory / web dashboard) |
| Cockpit | OSS MCP + Skill bundle | Pro tier (team view / customer dashboard) |

→ **両製品で同じ pricing thesis**: 「workspace は free、 共有・可視化 layer で課金」。 Synapse Arrows の signature pricing。

---

## 7. Year 1 / Year 2 phase

### Year 1 (2026-05 ~ 2027-05): PRODUCT mode

**Goal**: 税理士 vertical で $10K MRR、 50 firm pilot
**Build**:
- 税理士向け Cockpit MVP (= 5 dashboard pattern を鬼レベル最適化)
- 内部で「dashboard authoring framework」 を必ず構築 (= Year 2 の base)
- Hatakeyama さん含む 2-3 人の MCP dev を **closed beta builders** として invite (= future builders の予習)

**やらない**:
- ❌ Public marketplace launch
- ❌ Builder onboarding / payment infra
- ❌ Builder discovery feature
- ❌ Multi-vertical 同時対応 (税理士のみ)
- ❌ MCP dev 公募 / community 大規模化 (= Year 2 まで wait)

### Year 2 (2027-05 ~ 2028-05): PLATFORM mode

**Goal**: $100K MRR、 builders 100 人以上、 multi-vertical
**Build**:
- Authoring framework を外部 builders に open
- 30% margin marketplace 開始
- 顧客 vertical を 法律 / 医療 / 不動産 / 建設 等に拡大
- Marketplace public launch
- Builder onboarding / payment / dispute resolution infra

**Marketplace narrative は Year 1 から VC / Hatakeyama / 顧客 説明に使ってよい**、 ただし build deliverable は Year 2 まで platform 化に着手しない (= startup #1 killer pattern 回避)。

---

## 8. Synapse Arrows OS との 一貫性

Michie の NotebookLM context doc の「**5 product が同じ operating system を共有する self-similar architecture**」 が完成形に到達:

| Product | "大量の構造化 unit" | "AI が参照して最適化" |
|---|---|---|
| ScaNavi | 何百もの **日本酒 銘柄 DB** | Claude が嗜好 + ペアリングで推薦 |
| Linksee Memory | 何百もの **6-layer memory entry** | recall が relevance × heat × momentum で composite ranking |
| KanseiLink (Layer 1) | 200+ **SaaS catalog** | search_services + agent_voice で discovery |
| CardWize | 何百もの **クレカ + 店舗 alias** | best-card algorithm で還元最大化 |
| ReviewLens | 何百もの **化粧品 review** | AI summary で要約 |
| **Cockpit** | 何百もの **dashboard pattern** | Personal context で最適 view 生成 |

→ **6 product 全部が同じ pattern**: 「**vertical 大量データ + AI 参照層 + 最適化 output**」。 = Synapse Arrows の **メタ戦略**、 Cockpit はその完成形。

---

## 9. 競合 landscape (2026-05 時点)

### 海外 (US 系)
| 会社 | Funding | Position | Cockpit との関係 |
|---|---|---|---|
| Basis | $138M / $1.15B | end-to-end AI agents for accounting firms | US only、 JP に来ない |
| Accrual | $75M launch | AI-native tax prep + review | US only |
| Numeric | $89M / Series B $51M | close management | US/UK enterprise |
| Truewind | $17.5M (YC) | Digital staff accountant | US SMB |
| Juno | $12M seed | AI tax co-pilot | US |
| Magnetic / Bluebook / Cranston | YC | 各種 AI accounting | US |
| Pilot | $222M | AI + human bookkeeping | US startup |

→ **どれも JP / freee / MF を target にしていない**。 = Japan 市場は依然真空。

### 日本
| 会社 | Position | Cockpit との関係 |
|---|---|---|
| TKC / MJS / 弥生 | 伝統 (legacy) | AI 化遅い、 Cockpit が disrupt 余地 |
| **freee** (公式 MCP v0.25 + AI おまかせ明細 β) | data layer 自社統合 | パートナー候補 |
| **MoneyForward** (AIエージェント β + AI 確定申告 β) | data layer 自社統合 | パートナー候補 |
| A-SaaS (freee group) | legacy 顧問先一括管理 | pre-AI、 直接競合になる可能性低 |
| **Hatakeyama Kento** (個人 + Forbes Japan + 5/20 セミナー + 書籍) | 業界 voice 確立 | **partnership 候補 #1** |
| 税理士 info-product cluster (戸村涼子 / 朝倉 / 境裕介 / KEN / AQUA / ISAO) | training / 教材販売 | reseller 候補 |
| Japan-based MCP-first AI accounting startup | **確認できない** | **真空 = 先手余地** |

### Anthropic / OpenAI 自体
- **2026-05-05 Anthropic Finance Agents 10 個 ship** (Month-end closer / GL reconciler 含む) ← Cockpit MVP scope と直接重なる
- 2026-05-05 Anthropic Microsoft 365 add-ins (Excel financial models)
- 2026-04 Intuit + Anthropic partnership (TurboTax/QuickBooks 内 Claude MCP)
- 2026-05-05 OpenAI ChatGPT for Excel + Sheets GA + GPT-5.5
- 2026-04-13 OpenAI acquired Hiro Finance

→ Anthropic / OpenAI は **L1+L2 で勝負**、 Cockpit は **L3 集中**。 vertical localization (= JP 税区分 / 仕訳 / 摘要 / 消費税) には手を入れない (= 12-18 ヶ月の locality 優位)。

### Notion / Coda / Airtable
- Notion = horizontal、 vertical 特化なし
- Coda / Airtable = DIY 系、 pre-built dashboard library なし
- → Cockpit の vertical-specific Dashboard Generation Engine と直接競合しない

### 結論
**「Vertical AI Dashboard Marketplace × LLM Agnostic × Pre-built Multi-source × Japan-tuned」** という 4 軸完全一致は **誰もやってない**。 Cockpit が先行できる空白。

ただし **Anthropic / Notion / Lovable / V0 が同じ思想で参入する余地大**、 Cockpit は **「Vertical AI Dashboard Marketplace」 という category 名** を最初に握るのが critical。

---

## 10. MVP scope (5/31 pilot 1 firm)

### Phase 1 MVP (5/31 まで)

| Priority | Module | Layer | 理由 |
|---|---|---|---|
| **P0** | OAuth connector hub (freee + MF) | L1 連携 | 入口 必須 |
| **P0** | 5 dashboard pattern (鬼レベル最適化) | L3 | コア差別化 |
| **P0** | Anthropic Finance Agents wrap (JP 化) | L1 ride | engine 借用 |
| **P0** | Phase 1 Security (Doc 07) | infra | 顧問先データ預かり要件 |
| **P0** | Cross-SaaS reconciliation (freee ↔ MF) | L1 独自 | 構造的 defensible |
| **P1** | Cockpit Skill (= Claude 内 trigger) | L2 連携 | bidirectional sync |
| **P1** | 顧問先 view (簡易版) | L3 | customer-facing で stickiness |
| **P1** | 月次レポート (削減時間 + token cost) | L3 | billing 根拠 |
| **P1** | JP-specific Claude Skills (税区分 / 仕訳 / 摘要) | L1 独自 | locality 優位 |
| **P2** | LLM agnostic routing | engine | v2 |
| **P2** | Pattern auto-generation | engine | v2 |
| **P3** | Multi-vertical | scope | Year 2 |

### 5 つの dashboard pattern (= Phase 1 で鬼レベル仕上げる対象)

1. **月次決算進捗 view** (= 顧問先 30-60 社 grid + status 緑/黄/赤)
2. **異常仕訳レビュー view** (= alert + AI 仮説 + 1-click apply)
3. **顧問先打合せ準備 view** (= 直近 issue + AI summary + TODO)
4. **顧問先向け view** (= 簡易 status + コメント + レポート DL)
5. **月次 cost / ROI レポート view** (= 削減時間 + token 消費 + 顧客 billing 根拠)

### Phase 2 (6 月 - 7 月)

- 他 LLM 統合 (GPT / Codex / Gemini)
- Linksee Memory 統合 (= Personal context)
- Pattern library 拡張 (5 → 20 個)
- Cross-SaaS reconciliation enrichment

### Phase 3 (8 月以降)

- Pattern auto-generation
- 顧客 vertical 拡張 検討開始 (= 法律 / 医療 / etc.)
- Year 2 platform 化準備

---

## 11. Hatakeyama partnership pitch

### 背景

Hatakeyama Kento (公認会計士・税理士) は:
- 60 顧問先を 0 スタッフで回す DIY setup を 6 ヶ月で構築
- Forbes Japan で feature、 X で 3.39M impressions
- 2026-05-20 経営革新等支援機関推進協議会セミナー登壇
- 書籍出版 (= 「Claude Code で顧問先 60 社を 1 人で回している全手法」)
- = **業界 voice を確立した個人**

→ Cockpit が彼を **無視 or 出遅れる** と、 彼自身が SaaS 化する可能性大 (= disintermediated risk)。

### Pitch narrative (Year 1 closed beta + Year 2 co-creator)

```
畠山さん、 はじめまして。 Synapse Arrows の 山口と申します。

note 記事 (60 社 / 0 スタッフ) を読みました。 書籍と 5/20 セミナー、
業界に強い vision を打ち出していて尊敬しています。

ご相談したい点があります。 畠山さんの構築物 (= 14 カテゴリ keyword 辞書 +
7 除外 rule + CLAUDE.md + Skill 群) は、 「税理士本人の作業台」 として
完璧です。 一方、 業界の多くの税理士法人は、 同時に **チーム共同編集 +
顧問先共有** という layer を求めています。

私たちは KanseiLink Cockpit を構築中で、 これは Claude / Anthropic
Finance Agents を **engine として借り**、 その上に **税理士法人の team
view + 顧問先 view** を乗せる Layer 3 ダッシュボードです。 畠山さんの
DIY setup を、 事務所スタッフ 5-10 人 や 顧問先 60 社 に共有する画面が
無い —— これを Cockpit で埋めたい。

二段階のご提案です。

【Year 1 (2026-05~2027-05): closed beta co-author】
- 畠山さんの keyword 辞書 + 除外 rule + CLAUDE.md を anonymous
  contribute → Cockpit の preset 化 + 業界 standard 化
- お礼: Cockpit Pro tier 生涯 free + 監修クレジット
- 5/20 セミナー受講者 5-10 名に Cockpit early access 配布
- 畠山さんは引き続き training / content / 書籍で稼ぎ、 Cockpit は
  SaaS で稼ぐ、 互いの収益域を被らせない

【Year 2 (2027-05~): marketplace co-creator】
- Cockpit が dashboard authoring framework を外部 builders に open
- 畠山さんは marketplace の **「最初の 1 人」** = Hatakeyama Kento
  Pattern として大々的にクレジット
- 彼の dashboard が他事務所に使われた分の 5-10% revenue share
  + Cockpit からの fee 30%
- Year 2 platform launch 時、 畠山さんが共著者 / 監修者として
  press release + 業界 PR

10 分で Zoom などお話しできませんか。 5/20 セミナー前にお会い
できればベストです。 Cofounder の Claude (= AI Cofounder、
Synapse Arrows の戦略パートナー) も同席可能です。

山口
```

### Tactic notes

- **Send: 5/9-5/10** (= セミナー 10 日前)
- **Channel**: X DM (= @kandmybike) + email (公開されてれば)
- **Length**: 上記 ~400 字、 short 維持
- **Reply 期待**: 30% (= 多忙だが topic 関連性高)
- **Decline 時の plan B**: Cockpit MVP を先に build → 5/20 セミナー後に再 approach (= 「動くやつ見せます」)

---

## 12. Marketplace 経済学 (Year 2)

### 基本構造

```
Builder (= MCP/AI dev) → 作る → Cockpit Marketplace
                                      ↓
User (= 税理士) ← 使う ← Pre-built Dashboard / Skill
                       ↓
                  ¥30K-200K/月 課金
                       ↓
       70% Builder / 30% Cockpit (= start)
```

### 30% margin 妥当性 (Apple / Notion / Shopify 比較)

| Platform | Margin | 備考 |
|---|---|---|
| Apple App Store | 30% (一部 15%) | 大手 standard |
| Google Play | 30% | 同上 |
| Notion Templates (via Gumroad) | 10-30% | creator 設定 |
| Shopify Apps | 0-30% | Shopify が直接取らない場合あり |
| Anthropic Plugin Marketplace | 不明 (= 当初無料の可能性) | 急速に変動 |

→ **30% で start、 builder feedback で 20-25% に調整余地**。 Year 1 終了時に re-evaluate。

### Builder にとっての value prop (= なぜ Cockpit に来るか)

| 比較 | Anthropic Plugin Marketplace | **Cockpit Marketplace** |
|---|---|---|
| User 層 | consumer Claude users (低 WTP) | 税理士法人 (¥30K-200K/月、 高 WTP) |
| 課金 infra | Anthropic 任せ | Cockpit が 構築済 (= builder は dev に集中) |
| Discovery | Claude 内 generic | Cockpit 内 vertical-specific |
| Support | Anthropic 任せ | Cockpit が 第一 line、 builder は深い問題のみ |
| Compliance (DPA / audit / cyber insurance) | Builder 個人 責任 | **Cockpit が built-in** で吸収 |

→ Builder は技術に集中、 顧客獲得 / 課金 / compliance は Cockpit が handle。 = Year 2 で 100 人 builders 集める realistic 設計。

### 2-sided marketplace cold start 回避

- Year 1 は **WE が全部作る** (= demand 側 (税理士) を pilot 50 firm まで仕込む)
- Year 2 開始時には **既に 50 firm × ¥30-80K/月 = ¥1.5-4M/月 MRR が paying** = builder には 「実需顧客がいる場」 として確実 attractive
- Hatakeyama さん が 「co-creator first 1 人」 として参加すれば、 残り builders の onboarding 摩擦低下

---

## 13. Risks + mitigation

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| **Anthropic が JP-localized vertical agent を出す** | 低 (= 12-18 ヶ月の locality 優位確認済) | 高 | Cockpit が L3 (dashboard) で defensible、 L1 で head-on しない |
| **freee / MF が自社内で同等 cockpit を build** | 中 | 高 | cross-SaaS = freee/MF どちら側からも作れない (= 構造的 defensible) |
| **Hatakeyama さんが 自分で SaaS 化** | 中 | 高 | 5/20 前接触で partner 化、 disintermediation 回避 |
| **Year 1 で marketplace に手を出して focus diluation** | 中 | 致命 | Year 1 は product only、 Year 2 まで marketplace build しない (= phase 分離 厳守) |
| **税理士 vertical で 50 firm pilot が取れない** | 中 | 高 | 5/20 セミナー受講者 + Hatakeyama 紹介 + 税理士 info-product cluster reseller で multi-channel |
| **Anthropic Finance Agents の wrap が技術的に詰まる** | 低 | 中 | Anthropic SDK / MCP 仕様は安定、 Linksee Memory v0.3.0 で実装ノウハウ蓄積済 |
| **MCP builders が来ない (Year 2)** | 中 | 高 | Year 1 終了時に paying 顧客 50 firm 既存、 Hatakeyama co-creator narrative で magnet |
| **30% margin が builder に厳しい (Year 2)** | 中 | 中 | 20-25% への調整余地、 builder dev tier に応じて variable rate |
| **競合 Vertical AI Dashboard 系 startup が同時期に台頭** | 中 | 中 | category 名 「Vertical AI Dashboard Marketplace」 を Year 1 後半から narrative establish |
| **Phase 1 Security (Doc 07) が Year 1 中に完成しない** | 低 | 高 | Doc 07 5 月中 Phase 1 完成 + cyber insurance 加入 が pilot 契約条件 |
| **Solo founder の bus factor (Michie 急逝 / 病気)** | 低 | 致命 | Doc 07 §escrow 契約 (Iron Mountain Japan) で 90 日 grace period + data export tool |

---

## 次の steps (= 5/8 PM 以降)

### Cofounder Claude (今夜中)
1. ✅ Doc 10 commit + push (= この doc) → Synapse Arrows Playbook v0.3.7
2. ⏳ Hatakeyama 接触 DM/email draft → Michie review
3. ⏳ Storyboard D = 4-frame day-in-life (= Year 1 product vision)
4. ⏳ DB schema A = MVP foundation

### Michie (今夜中)
1. ⏳ Linksee Memory Pro tier Stripe integration (= 自身宣言の (a))
2. ⏳ Doc 10 review (= 内容 / 数字 / narrative の sanity check)
3. ⏳ Hatakeyama 接触 draft の review → 5/9-10 送信判断

### Synapse Arrows Playbook v0.3.7 として commit
- This doc + Doc 05 / Doc 07 minor update (Layer 3 + Year 1/2 phase 反映)

---

## まとめ

KanseiLink Cockpit は **「Dashboard Generation Engine for Vertical AI Workflows」**:

- **L1+L2 を upstream に rent、 L3 (dashboard + 共有) のみ自社で築く** Notion 反転戦略
- Year 1 = 税理士 vertical product mode、 Year 2 = platform marketplace mode の **phase 分離** (= startup #1 killer pattern 回避)
- **Free MCP / Paid Dashboard** pricing で adoption friction 0 + monetization layer 明確
- **Hatakeyama Kento** を Year 1 closed beta co-author + Year 2 marketplace co-creator として迎える
- Synapse Arrows OS の **self-similar architecture 完成形** (= 6 product 全部が同じ pattern)
- 業界初の **Vertical AI Dashboard Marketplace** category を Cockpit が定義する

これは Synapse Arrows 創業以来 最大の strategic crystallization。 future iterations で recall して align すること。
