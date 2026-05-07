# KanseiLink — Finance Vertical Pivot (3-Layer Strategy, May Sprint)

> Status: strategic pivot, 2026-05-07 起案 → **2026-05-07 PM May Sprint mode** (4-6週 → 1-2週)
> Owner: Michie (B2B sales) + Cofounder Claude (strategy)
> Predecessors: 既存 KanseiLink MCP intelligence layer (200+ Japanese SaaS catalog)
> Companions: [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md), [06-tokyo-conference-strategy](./06-tokyo-conference-strategy.md), **[07-kansei-link-cockpit-security-posture](./07-kansei-link-cockpit-security-posture.md) (security 別 doc に切り出し)**

## 🔴 2026-05-07 PM 重要更新: May Sprint mode + Doc 07 分離 + Zero-Infra 検討

### (1) May Sprint mode

Michie 確認 (5/7): 「計画が遅すぎる。 1-2 日で実装してそこから拡散、 全部 5 月で終わらせる」

→ Cockpit MVP は **4-6 週 → 2 週圧縮** (Phase 1 security と並行)。
→ ICP-A pitch は 5/26 から、 pilot 1 firm 契約は 5/31 までに目指す。

### (2) Security posture を Doc 07 に独立分離

会計事務所向けの購買決定 trigger は機能ではなく **「データを預けて大丈夫か」** の信頼判断。
別 track の重要性が増したため → **Doc 07** として分離: `07-kansei-link-cockpit-security-posture.md`

→ Layer 3 Cockpit 章のすべての security 関連は **Doc 07 を参照** とする。

### (3) Zero-Infra vs Self-host with Security の判断

サーバー保有リスク (DDoS / ransomware で個人開発 SaaS が廃業する事例) を踏まえた検討の結果:

| 選択肢 | 採否 | 理由 |
|---|---|---|
| **Zero-Infra** (Layer 3 を BYO Vercel テンプレ配布) | ❌ 不採用 | 会計士 / 税理士は "気軽に web で使える" UX を期待。 self-host は friction 過剰、 問い合わせ対応も難。 |
| **Self-host with Phase 1 Security** (Vercel JP + Supabase JP + Cloudflare + insurance + audit log + DPA) | ✅ **採用** | Doc 07 で詳細化。 月 ¥45-100K で 1 顧客で回収、 unit economics 成立。 |
| **Hybrid** (Layer 1 = git+CDN / Layer 2 = npm runtime / Layer 3 = managed self-host) | ✅ **副採用** | Layer 1-2 は user runtime / static で軽量、 Layer 3 のみ自社 host 集中。 |

→ Layer 3 だけ自社 host、 ただし Phase 1 Security (Doc 07) で堅守する設計。 Layer 1-2 は user runtime / git+CDN で攻撃面最小化。

### May Sprint timeline (圧縮版、 Cockpit + Phase 1 security 並行)

| Week | 期間 | Layer 1 (catalog) | Layer 2 (Finance MCP) | Layer 3 (Cockpit + Security) |
|---|---|---|---|---|
| **Week 1** | 5/7 - 5/12 | git+CDN 移行検討 | J-GAAP Earnings Reviewer 実装 | Vercel/Supabase/Cloudflare 契約 + DB schema (Doc 07 §Phase 1 Day 1-7) |
| **Week 2** | 5/13 - 5/19 | catalog 公開継続 | Month-end Closer 実装 | 2FA + audit log + 削除証明書 (Doc 07 §Phase 1 Day 8-14) |
| **Week 3** | 5/20 - 5/26 | (静的化保留) | Statement Auditor 実装 | ICP-A 5 firm pitch + DPA 提示 + 法務 finalize |
| **Week 4** | 5/27 - 5/31 | (拡散) | (拡散) | **pilot 1 firm 契約目標** + Online Demo Day demo segment 準備 |
| **Bonus** | 6/1 - 6/9 | catalog 拡大 | + Sansan / SmartHR 連携 | pilot data validation + 第2 firm pitch |
| **Peak** | 6/10 | Online Demo Day で全 Layer demo (22:00 JST) |

## 2026-05-07 PM sharpen (重要な修正)

当初の 2層構造案 (Layer 1 Composio + Layer 2 Finance MCP) は **MCP dev 向けの発想に止まっていた**。 実際の市場 (税理士・会計士・SMB 経理担当) は MCP server を直接設定できない、 Claude / GPT に顧客データを直接流せない (security 怖い)、 自前で組む時間 / skill ない。

→ **deliverable は Web UI (SaaS 風 dashboard)**、 MCP は backend に隠す。

3層構造に進化:
- Layer 1 (基盤): Japanese Composio (200+ SaaS catalog、 既存)
- Layer 2 (拡張): Finance Vertical MCP server (J-GAAP Earnings Reviewer / Month-end Closer / Statement Auditor)
- **Layer 3 (NEW): Cockpit Web UI for tax accountants** (= 営業可能 product)

新名称 (内部): "**KanseiLink Cockpit**"

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

## Strategic positioning (3層構造)

### Layer 1 (基盤): Japanese Composio

200+ Japanese SaaS catalog + MCP intelligence + recipe / agent_voice / audit_cost。
**変えない**。これが kansei-link.com の実体。

### Layer 2 (中間): Finance / Accounting Vertical MCP

Layer 1 の上に **特化 MCP server** を 3 つ build:
1. **J-GAAP Earnings Reviewer** — TDnet / EDINET 資料 → freee 連携 → AI summary
2. **Month-end Closer for 会計事務所** — 弥生 / freee の月次決算 AI 自動化
3. **Statement Auditor for 経費精算** — freee 経費 → 異常検知 + 異議メモ

これらは **Anthropic の global tools の Japan ブリッジ** として positioning。
ただし**最終ユーザー (税理士) には見えない**。 dev / 内部統合用。

### Layer 3 (NEW、 営業面): Cockpit Web UI

```
Persona: 個人税理士 / 会計事務所 / 中小企業経理担当
         (= 技術者ではない、 freee / Money Forward を毎日使う人)

Product: Web UI (familiar SaaS look) で AI が下働き
         backend は Layer 1 + Layer 2 (MCP server)

Value:   "面倒な経理 work が AI でやれる、 でも顧客データは安全"
         = market barrier 3 つを全部解消

Channel: SaaS subscription (per firm or per seat)
```

#### Architecture

```
┌──────────────────────────────────────────┐
│ Layer 3 (NEW): Cockpit Web UI            │
│  ・ Login + dashboard                     │
│  ・ Workflow tile (J-GAAP Earnings 等)    │
│  ・ Audit log + 顧客データ管理             │
│  ・ Web app は Vercel (Japan region)      │
└──────────────────────────────────────────┘
           ↑ HTTPS / GraphQL (server only call)
┌──────────────────────────────────────────┐
│ Layer 2: Finance Vertical MCP server     │
│  ・ Sampling で Anthropic Claude 経由     │
│  ・ Layer 1 catalog 経由で freee 連携     │
└──────────────────────────────────────────┘
           ↑ MCP protocol (internal)
┌──────────────────────────────────────────┐
│ Layer 1: Japanese Composio               │
│  ・ 200+ SaaS catalog (既存)              │
│  ・ recipe / agent_voice / audit_cost    │
└──────────────────────────────────────────┘
```

→ **税理士は Layer 3 だけ見える**、 Layer 1-2 は完全に隠蔽。
"AI を意識せず使える" = adoption barrier 消滅。

#### なぜ Web UI 必須か (3 つの構造的 barrier 解消)

| Barrier | 旧 plan (raw MCP) では解けない | Cockpit Web UI で解ける |
|---|---|---|
| AI 自動化の knowledge ない | dev 必要 | dashboard click だけ |
| 顧客データ流出 risk | client 側に Claude key 必要 | Synapse Arrows サーバー (日本) 経由、 audit log + 即時削除 |
| 自分で組む時間 / skill ない | 各事務所が個別に MCP server 設定 | 即 onboarding (signup → 5 分で workflow 動く) |

#### Security narrative (商品化できる)

```
あなたの顧客データは:
  1. Synapse Arrows のサーバー (日本 region) を一時通過
  2. Anthropic Claude API に渡る (匿名化 layer 経由)
  3. 完了後即削除 (no training data)
  4. 全 access は audit log に記録 (監査対応)
  5. SOC 2 / ISMS 準拠ロードマップ (Phase 3 で対応)
```

これは MCP server を直接立てる場合 **技術的に提供不可能** (client 側 token 経由なので Synapse Arrows が gate できない) だった。 Cockpit で **間接化** すれば security guarantee を商品化できる。

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

### ICP-A: 会計事務所 (1-30人規模) ← **Phase 1 main target**

**Pain**:
- 月次決算で同じ作業を毎月繰り返す
- 顧客企業 50-200社の経理データを横断
- freee / Money Forward / 弥生 を顧客毎に切替え
- 月末の閉め作業が一週間集中
- AI 試したいが顧客データを Claude に直接入れられない

**Cockpit Web UI の value**:
- 月次 close routine の AI 自動化
- 顧客 × 過去 N か月の異常検知
- 「いつもと違う仕訳」 alert
- **顧客データ流出 risk なし** (Japan region + audit log)
- **value prop**: 「月次決算が3日 → 1日に、 顧客データも安全」

**価格 hypothesis** (Cockpit Web UI tier):
- Early bird (Phase 1): ¥30K-50K / 月 / 事務所
- 通常: ¥75K-100K / 月 / 事務所
- 大規模 (10+ accountants): ¥150K-200K / 月 / 事務所

**Sales motion**: 既存知人 / 紹介 / 会計事務所コミュニティ / freee partner program / Note 発信者

### ICP-B: 個人 CFA / 投資銀行アナリスト / 個人投資家

**Pain**:
- TDnet / EDINET 大量資料を読む必要
- Excel で財務モデル毎回ゼロから
- 競合ベンチマーク調査が労働集約

**Cockpit Web UI の value**:
- 開示資料 → 財務モデル自動生成
- 業界ベンチマーク 比較 (200+ SaaS 横断)
- Microsoft 365 連携 (Excel → PPT → Outlook flow)
- Web UI で one-click

**価格 hypothesis**: ¥10K-30K / 月 / 個人
**Sales motion**: X / Note 個人発信 + financial vertical community

### ICP-C: 中小企業 経理担当 (50-300人規模)

**Pain**:
- freee / 弥生 の使いこなし足りない
- 経費精算の異常検知 (不正 or 入力ミス)
- 月次レポート作成

**Cockpit Web UI の value**:
- 経費自動 audit (Web UI で alert を確認するだけ)
- 月次 close 半自動化
- AI assistant 搭載 ("freee の使い方教えて")

**価格 hypothesis**: ¥50K-100K / 月 / 企業
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

## 6か月後 (2026-11) の想定 state (Cockpit Web UI 含む)

| 指標 | 現状 (5/7) | 6か月後 target |
|---|---|---|
| KanseiLink Cockpit paying firms | 0 | **20-30** |
| Cockpit MRR | $0 | **$10K-15K** (¥150-220万 月商) |
| ICP-A (会計事務所) pilot | 0 | 5-10社 |
| ICP-B (個人 finance pro) | 0 | 50-100人 |
| ICP-C (中小企業) | 0 | 5-10社 |
| ARR | $0 | $120-180K |

**月 $10K MRR 達成 = bootstrap "勝ち" 第一段階**。

価格再計算:
- 旧 plan ($30K/mo × 5社 = $150 ≒ ¥22K MRR、 達成までの社数多い)
- **新 plan (Cockpit Web UI)**: ¥75K-200K/mo × 10-20社 = **¥750K-4M MRR ($5K-25K)**
  → bootstrap "勝ち" $10K MRR は 15社で達成可能

## Sales motion plan (Cockpit Web UI 中心)

### Phase 1 (5月-6月): Tokyo Conference 中心の早期 anchor 取り

- Cockpit Web UI MVP 構築 (Workflow 1: J-GAAP Earnings Reviewer のみ)
- Tokyo Conference 6/10 で 5-10社 contact、 demo 見せる
- 1社が pilot に乗ったら anchor → case study 化
- pilot 中の friction 全部 product 改善 input

#### Pilot offer (early bird)

```
30日 free trial → ¥30K/mo (early bird、 通常 ¥75K) で 6か月固定
代わりに:
  ・ 使用感 feedback weekly call
  ・ case study に名前 / 事務所名 OK
  ・ 紹介 1 件で月額 半額 (= ¥15K) 1年間
```

→ early adopter は安く、 紹介で grow という SaaS 標準 motion。

#### Tokyo Conf reach メッセージ案

```
"freee/MF 使う税理士向けに、 日本会計対応の AI cockpit を作っています。
 顧客データを直接 Claude に流さず、 セキュアな bridge layer 経由で
 J-GAAP 決算 review / 月次 close / 経費 audit を自動化します。
 Tokyo Conf 6/10 で demo します、 早期 pilot 価格は ¥30K/mo
 (通常 ¥75K) です。"
```

### Phase 2 (7月-8月): 紹介経由の expand + Workflow 拡充

- Workflow 2 (Month-end Closer) Web UI 公開
- Workflow 3 (Statement Auditor) Web UI 公開
- pilot 1社が working → 同業 (会計事務所コミュニティ) で口コミ
- ICP-A 会計事務所 5-10社 pilot 目標
- ICP-B 個人 finance professional は X / Note で個人発信

### Phase 3 (9月-): SMB outbound + Cockpit feature 拡充

- ICP-C 中小企業を targeted outbound
- Cockpit に経費自動 audit / 月次レポート機能追加
- 月 $10K MRR 達成検証

### Phase 4 (Q4 以降): Cockpit Pro tier

- multi-firm management (複数事務所横断)
- API access (Cockpit を他 SaaS から呼べる)
- 月 $50K MRR を目指す

## 既存資産との接続性 map

```
[現 KanseiLink (Layer 1 + 2)]
  ├── search_services tool        → Layer 2 product 全部で活用
  ├── get_recipe tool              → freee/弥生 連携 recipe を vertical 用に拡張
  ├── audit_cost tool              → Statement Auditor の前身、 finance 向け再設計
  ├── agent_voice tool             → finance professional voice 収集に転用
  ├── reconnaissance ant           → Statement Auditor の monitoring 部分に流用
  └── KanseiLink web dashboard     → Cockpit Web UI (Layer 3) の base に流用

[新 Layer 2 finance MCP]
  ├── J-GAAP Earnings Reviewer     ← TDnet/EDINET parser 新規
  ├── Month-end Closer             ← Microsoft 365 連携新規
  └── Statement Auditor            ← reconnaissance ant 流用

[新 Layer 3 Cockpit Web UI]
  ├── Login + Auth                 ← Supabase 流用
  ├── Dashboard (workflow tile)    ← Next.js + Vercel
  ├── Workflow runner              ← Layer 2 MCP server を backend で叩く
  ├── Audit log viewer             ← Supabase Postgres
  └── Settings / Billing           ← Stripe (linksee.com で実績)
```

### Cockpit Web UI 技術 stack

```
Frontend:    Next.js 16 + Tailwind (KanseiLink website 既存知見)
Backend:     Next.js API routes / Supabase Edge Functions
Auth:        Supabase Auth (Magic link / Google OAuth)
Database:    Supabase Postgres (Japan region)
Storage:     Japan region (Supabase JP) で顧客 data
Payments:    Stripe (Linksee Memory Pro tier と共有)
LLM:         Anthropic Claude (server side、 Sampling 経由)
MCP server:  既存 KanseiLink (kansei-link-mcp-production.up.railway.app)
            Cockpit backend が MCP client として叩く
Hosting:     Vercel (Japan region で deploy)
```

### Solo 実装なら 4-6 週間で MVP

```
Week 1-2: Auth + Dashboard skeleton + Workflow 1 のみ実装
Week 3-4: Layer 2 MCP server build (J-GAAP Earnings Reviewer)
Week 5:   Stripe + audit log + Japan region 設定
Week 6:   Pilot 開始 (1社)、 friction を Phase 2 input
```

→ Tokyo Conference 6/10 までに **Workflow 1 (J-GAAP Earnings Reviewer) の Cockpit demo は間に合う**。

## Risk & mitigation

| Risk | Mitigation |
|---|---|
| Composio が Japan 進出して generic 領域で attack | finance vertical 先行 = 競合せず差別化 (Stripe vs GMO の関係) |
| Anthropic 自身が J-GAAP 対応 | unlikely (vertical 特殊性高すぎ)、 仮に来ても KanseiLink は SMB 向け |
| 会計事務所 sales cycle が長い | pilot 価格 ¥0-10K で friction ゼロにする |
| 単一 founder で営業 capacity 限界 | Cofounder Claude が pre-sales / RFP / proposal 自動化 |
| 金融 vertical 特化で "general MCP" brand 失う | Layer 1 (Japanese Composio) を維持、Layer 2 が "first product" |

## DECISIONS log

### 2026-05-07 PM (sharpen) — Cockpit Web UI を Layer 3 として追加

**CONTEXT**:
当初の 2層構造 (Layer 1 Composio + Layer 2 Finance MCP) は MCP dev 向け発想に止まっていた。 Michie の市場観察 (5/7 PM):

```
✅ Freee 使う会計士・税理士が SNS で workflow 発信している
✅ 同じ人達が MCP 自動化を試して失敗
✅ "人力でやるの面倒" の声が広い

❌ AI 自動化の knowledge ない
❌ 顧客データ流出 risk (Claude/GPT に直接入れるの怖い)
❌ 自分で組む時間 / skill ない
```

→ 「raw MCP server を税理士に渡す」 plan は構造的に営業不可能と判明。

**DECISION**:
3層構造に進化:
- Layer 1 (基盤): Japanese Composio (変更なし)
- Layer 2 (中間): Finance Vertical MCP server (内部統合用、 dev 向け)
- **Layer 3 (NEW): Cockpit Web UI for tax accountants** (営業 product)

新名称 (内部): "**KanseiLink Cockpit**"

**REASON**:
1. **Sales motion 革命**: dev 向け MCP server 設定 → Web SaaS subscribe で営業対象が万人規模に
2. **価格上昇**: ¥10-30K/mo dev tier → ¥75-200K/mo business tier
3. **Security narrative 商品化**: MCP では不可能だった "Japan region + audit log + 即時削除" guarantee が成立
4. **Tokyo Conf demo が強力化**: CLI MCP demo (技術者のみ刺さる) → Web cockpit (誰でも理解できる)

**REVERSIBILITY**:
Medium — Layer 3 (Cockpit) を撤退すれば Layer 1+2 (基盤 + MCP) に戻れる
ただし税理士向け marketing 後の方向転換は brand コスト

**OPEN QUESTIONS**:
- Cockpit MVP の Workflow 1 (J-GAAP Earnings Reviewer) は 4-6 週間で間に合うか?
- Pilot 価格 ¥30K vs ¥50K (early bird) でどちらが signup multiplier 高いか?
- Audit log / SOC 2 / ISMS の compliance roadmap は Phase 3 で間に合うか?
- 顧客データ Japan region 縛りは Vercel + Supabase 構成で十分か?

### 2026-05-07 AM — Finance Vertical Pivot 決定

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
