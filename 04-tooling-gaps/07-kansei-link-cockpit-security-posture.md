# KanseiLink Cockpit — Security Posture (Phase 1-3)

> Status: 策定、 2026-05-07 起案 (May Sprint mode)
> Owner: Michie (戦略 + 弁護士 / insurance) + Cofounder Claude (実装 checklist)
> Companions: [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md), [04-linksee-memory-pro-tier-launch-plan](./04-linksee-memory-pro-tier-launch-plan.md)

## なぜ Doc 07 が独立して存在するか

KanseiLink Cockpit (Layer 3 Web UI) は **会計事務所・税理士向け** の SaaS。
この segment の購買決定 trigger は機能ではなく **「データを預けて大丈夫か」** という信頼判断。
セキュリティ実装は機能と並行して走る別 track。 Doc 05 から security 章を切り出して独立 doc 化。

### 4 つの警戒ポイント (顧客視点)

| 警戒 | 顧客の不安 | 我々の答え |
|---|---|---|
| **データ漏洩** | 顧問先の決算情報が外に出る | encryption at rest / TLS 1.3 / RLS / audit log export |
| **改ざん** | 試算表が不正書換される | append-only audit log + DB trigger + PITR |
| **可用性** | 月次決算期にダウン | Vercel + Supabase + Cloudflare の multi-managed redundancy |
| **規制対応** | 個人情報保護法・業務上の秘密 | DPA + Privacy Policy + 弁護士 review + cyber insurance |

---

## 結論 — Solo founder で「100% 万全」は無理。 「業界平均より上 + 事故っても傷が浅い」 は achievable

Phase 1 だけで会計事務所に堂々と説明できるラインに到達できる。
Phase 2 で 大手事務所 (50人 firm / Big 4 系列) との契約交渉に入れる。
Phase 3 は ¥10M MRR 後 optional。

---

## Phase 1: MVP launch 必須 (May Sprint で 1-2 週、 ¥45-100K/月)

| 領域 | 実装 | コスト/月 |
|---|---|---|
| **Edge / DDoS** | Cloudflare Pro plan (WAF + Bot Management + Rate Limit) | $20-200 |
| **Hosting** | Vercel (JP region 必須) | $20-100 |
| **DB** | Supabase JP region + Row Level Security (RLS) で tenant 分離 | $25-100 |
| **暗号化** | TLS 1.3 only / DB at-rest encryption (Supabase 標準) / 機密項目は列レベル暗号化 | ¥0 |
| **認証** | 2FA 必須 (TOTP) + magic link / passwordless / SSO option | ¥0 |
| **Audit log** | DB trigger で全変更を append-only log table + 月次 S3 export | ¥0 |
| **Backup** | Supabase PITR 7日 + 週次 cold storage (encrypted) | $25 |
| **Secret 管理** | Vercel env + 3ヶ月 rotation (npm pattern と同じ — Linksee Memory に caveat あり) | ¥0 |
| **依存脆弱性** | Dependabot + Snyk + npm audit 自動 PR + GitHub Advanced Security | ¥0-$15 |
| **Cyber insurance** | 損保ジャパン / AIG / Tokio Marine の中小企業向け (¥1億補償) | ¥30-50K |
| **規約 / Privacy** | 個人情報保護法 23 条 委託 + 業務委託契約 (DPA) + Privacy Policy 弁護士 review | one-shot ¥30-50万 |

**Phase 1 月次 ranning**: $90-450 + ¥30-50K (insurance) ≒ **¥45-100K/月**
**Phase 1 one-shot 法務**: ¥30-50万 (5月中に弁護士 retain → review → 6月初 finalize)

### Phase 1 で言える marketing message

> 「データは Vercel JP / Supabase JP region で **日本国内 hosting**。
> Cloudflare で **DDoS / WAF / Bot 防御**。
> **2FA 必須**、 全操作 **audit log で記録 + 顧客 export 可能**。
> **PITR 7 日 rollback** 可能。 **サイバー保険 1億 加入済**。
> 規約 / DPA は弁護士 review 済、 **個人情報保護法 23 条 委託関係** に準拠。」

これは中小企業会計 SaaS 平均より **明確に上**。 freee / MoneyForward 級ではないが、 「会計事務所 SaaS」 segment では十分競争力。

### Phase 1 May Sprint Implementation Checklist

| # | Task | Day | Owner |
|---|---|---|---|
| 1 | Cloudflare Pro plan 契約 + DNS 移管 | Day 1 | Michie |
| 2 | Vercel JP region project 作成 (cockpit.kansei-link.com) | Day 1 | Cofounder |
| 3 | Supabase JP region project 作成 + RLS skeleton | Day 1 | Cofounder |
| 4 | DB schema + audit_log table + trigger 設計 | Day 2 | Cofounder |
| 5 | 2FA (TOTP) + passwordless flow 実装 | Day 2-3 | Cofounder |
| 6 | Audit log export (CSV / JSON) endpoint 実装 | Day 3 | Cofounder |
| 7 | Encryption at rest 確認 + 機密列の column-level encryption | Day 3 | Cofounder |
| 8 | Dependabot / Snyk / GitHub Advanced Security 有効化 | Day 4 | Cofounder |
| 9 | Cyber insurance 見積依頼 (3社) → 加入 | Day 4-7 | Michie |
| 10 | 弁護士 retain (Privacy Policy / DPA / 規約 review) | Day 4-10 | Michie |
| 11 | PITR + 週次 cold backup S3 + restore drill | Day 5 | Cofounder |
| 12 | Secret rotation runbook (3ヶ月 cycle) | Day 5 | Cofounder |
| 13 | Status page (Cloudflare Workers ベース) 公開 | Day 6 | Cofounder |
| 14 | Security page (cockpit.kansei-link.com/security) 公開 | Day 7 | 両者 |

---

## Phase 2: 顧客 5-10 firm 達成後 (6ヶ月以内、 = 2026-11 目標)

| 領域 | 実装 | コスト |
|---|---|---|
| **SOC 2 Type I** | Vanta or Drata で自動化 + 監査人 (US 系 firm で OK) | $15-25K (one-shot) + $500/月 |
| **Pentest** | 年 1 回、 日本の専門家 (GMO Cybersecurity / SecureSky / LAC) | ¥150-300万/年 |
| **Bug bounty** | HackerOne or YesWeHack の private program、 月 $500-1000 報奨 | $1-3K/月 |
| **個人情報保護法 PIA** | Privacy Impact Assessment (弁護士同伴で実施) | one-shot ¥30万 |
| **BCP / DR plan** | 文書化 + 年 1 回 drill (1 day) | 自前 |
| **Vendor Security Review** | Vercel / Supabase / Cloudflare の SOC 2 / ISO 27001 報告書取得 + 整理 | ¥0 |

### Phase 2 で言える marketing message (追加)

> 「**SOC 2 Type I attested** (Vanta 自動化 + US 監査人)。
> 年 1 回 **第三者 pentest** 実施 (日本 GMO Cybersecurity)。
> **bug bounty program** 稼働。 **PIA 実施済** (個人情報保護法 24 条 取得時利用目的の通知)。」

これで Big 4 系列の地方拠点 / 中堅事務所 (50-200 人 firm) との交渉に入れる。

---

## Phase 3: ¥10M MRR 後 (Optional、 enterprise 要件次第)

- **SOC 2 Type II** (audit period 6-12 ヶ月、 ~$30-50K + $1K/月 ongoing)
- **ISO 27001** 認証 (~¥500万-1000万、 12-18 ヶ月 prep)
- **24/7 monitoring** (PagerDuty + Datadog + on-call rotation = 人を雇う)
- **専任 security engineer** hire
- **Pen-test 年 2 回** + Red Team exercise

→ ¥10M MRR (= 月 50-100 firm × ¥10-20万 平均) 達成までは Phase 3 は不要。

---

## "100% は無理" な部分 — 残るリスクと吸収策

| 残るリスク | 吸収策 |
|---|---|
| **Zero-day** (Vercel / Supabase / Cloudflare 側) | 信頼するしかない。 SLA + insurance で経済リスクは限定 |
| **Social engineering** (Michie が phishing で credential 漏洩) | **YubiKey 物理 2FA** 必須 + 1Password + 操作 log + IP 制限 + email alias 分離 |
| **Insider 脅威** (Michie 自身が malicious actor の可能性) | …これは構造的に防げない。 **透明性** (audit log の顧客 export + 全 admin 操作 log) で代替 |
| **3am incident** (solo は寝てる) | Cloudflare auto-mitigation + PagerDuty 緊急 escalation + insurance の downtime 補償 + 公開 status page で透明性 |
| **小さな bug が暴露** | bug bounty + dependabot + 年次 pentest でカバレッジを上げる、 さらに **Privacy Policy で transparent breach notification 24h SLA** を約束 |
| **倒産 / Michie 急逝** | **Escrow 契約**: Source code + DB schema を第三者 escrow、 顧客向けに「90 日 grace period + data export tool」 約束 (bus factor mitigation) |

---

## 会計士業界 specific 配慮 (3 つ + escrow)

### (1) "委託元 - 委託先" 関係を契約で明確化

- **個人情報保護法 23 条**: 会計事務所が中小企業 (顧問先) のデータを KanseiLink に "委託" する形
- **業務委託契約書 (DPA = Data Processing Agreement)** を弁護士 review で整備
- これがないと会計事務所は契約できない (顧問先への説明責任)
- **DPA 必須項目**:
  - 委託の範囲 / 目的
  - 委託先の安全管理措置
  - 再委託の禁止 or 事前承認 (Vercel / Supabase 等の sub-processor list 開示)
  - 漏洩時の通知義務 (24h SLA)
  - 契約終了時のデータ削除 + 削除証明書
  - 監査権 (顧客が KanseiLink を audit する権利)

### (2) "データ消去保証" を機能として持つ

- 会計事務所が顧問先と契約終了 → 該当 tenant の全データ削除 + **削除証明書 PDF 発行**
- これは **機能 = 営業武器**。 freee / MoneyForward でも顧客側削除は manual。
- 削除 trigger: API endpoint + Cockpit UI のボタン
- 削除内容: DB rows + S3 backup + audit log の該当部分 (audit log の「削除した」事実は永続)
- 削除証明書: PDF (削除日時 / tenant ID / 削除した行数 / SHA-256 hash chain)

### (3) Audit log を顧客が直接 export 可能に

- 「KanseiLink が中で何やってるか会計士が透明に見える」設計
- Stripe Dashboard 風: 全 API 呼び出し / 全データ変更 / 全管理者 access が log で見える
- **これが信頼の核**
- 顧客視点の effect: 「Solo founder だから危険」 ではなく 「Solo founder だから透明」 に narrative 転換
- 実装: audit_log table に trigger ですべて記録 → REST + CSV export + 月次自動 email PDF report

### (4) Escrow 契約 (bus factor mitigation)

- Source code + DB schema を第三者 escrow (例: Iron Mountain Japan / 国内 escrow agent)
- 倒産 / 急逝 / 廃業 時の trigger 条件を契約に明記
- 顧客向けに「90 日 grace period + data export tool 自動配布」 を約束
- 会計事務所には「solo founder の事業継続性」の懸念に対する **構造的回答** として刺さる
- 実装コスト: ¥10-30万/年

---

## 勝ち筋の核 — 3 つの非対称性

### (1) Solo だから「透明・迅速」が言える

- Composio / Mem0 のような funded SaaS は会計事務所に「我々の中身は見せられない」と言わざるを得ない (組織内動線が複雑だから)
- Solo は audit log export + escrow 契約 + 削除証明書で逆に "全部見せます" と言える
- これは **regulated 業界では強い**

### (2) Phase 1 月次 ¥45-100K = Cockpit 1 顧客 (¥30-200K/mo) で回収

- 顧客 1 firm 取れた瞬間 unit economics が黒
- raise しなくても security に投資できる
- これは資金調達した競合が逆に苦しむ価格構造 (彼らは ¥100M/月 burn を 4 億顧客で割らないと黒にならない)

### (3) "日本会計事務所 specific 知識" + "Phase 1 security" の組み合わせが defensible

- **個人情報保護法 23 条 委託関係 の DPA** (= 弁護士 retain で身につく知識)
- **月次決算 cycle / J-GAAP 知識 / 税理士法対応** (= 業界経験で身につく知識)
- どれも US 系 SaaS が後追いで身につけにくい
- Phase 1 security はそこへの "入場券"、 業界知識が "席を取る武器"
- このコンボは Composio / Mem0 が日本会計事務所市場を取りに来ても **最低 12-18 ヶ月遅れる構造**

---

## Synapse Arrows Playbook v0.4 への昇格 candidate

この Doc 07 の方法論は KanseiLink Cockpit だけでなく:
- Linksee Memory **Team / Enterprise tier** (Doc 04 後継)
- ScaNavi B2B **飲食店 cockpit**
- CardWize **法人カード比較 enterprise**
- ReviewLens **化粧品ブランド enterprise**

すべての Synapse Arrows enterprise tier 共通の **"Phase 1 Security Boilerplate"** に昇格させる候補。
v0.4 の追加章として「Synapse Arrows Security Posture Standard」を 04-tooling-gaps から 共通章 (00-philosophy 内) に移す。

---

## 月次 cost 整理

| Phase | Monthly | One-shot | 顧客 break-even (¥30K-200K/mo Cockpit tier 想定) |
|---|---|---|---|
| Phase 1 | ¥45-100K | ¥30-50万 (法務) | **1 firm で回収** |
| Phase 2 | +¥30-50K (SOC 2 ongoing + bug bounty + pentest 月割) | +¥250-350万 (SOC 2 Type I + PIA + pentest 初年度) | **5-10 firm で回収** |
| Phase 3 | +¥200-500K (24/7 monitoring + security eng) | +¥1000-1500万 (ISO 27001 + SOC 2 Type II) | **30-50 firm で回収** |

---

## Action 直近 30 日 (May Sprint, 5/7 → 6/7)

### Week 1 (5/7 - 5/12)
- [ ] 弁護士 retain (Privacy Policy / DPA / 規約 review) — Michie
- [ ] Cyber insurance 見積依頼 (損保ジャパン / AIG / Tokio Marine) — Michie
- [ ] Vercel JP / Supabase JP / Cloudflare Pro 契約 — Cofounder
- [ ] DB schema + audit_log + RLS skeleton — Cofounder
- [ ] cockpit.kansei-link.com staging 稼働 — Cofounder

### Week 2 (5/13 - 5/19)
- [ ] 2FA + passwordless flow 実装 — Cofounder
- [ ] Audit log export + 削除証明書 PDF 生成 — Cofounder
- [ ] Cyber insurance 加入 — Michie
- [ ] 弁護士 review 完了 → DPA / Privacy Policy / 規約 finalize — Michie
- [ ] Status page + Security page 公開 — 両者

### Week 3 (5/20 - 5/26)
- [ ] ICP-A 5 firm に Phase 1 security pitch + DPA 提示 — Michie
- [ ] Escrow 契約検討 (bus factor mitigation) — Michie
- [ ] PITR + restore drill 実施 + runbook 作成 — Cofounder
- [ ] Secret rotation runbook 作成 (3ヶ月 cycle) — Cofounder

### Week 4 (5/27 - 5/31)
- [ ] **Cockpit + Phase 1 security 一体での pilot 1 firm 契約** — Michie
- [ ] Online Demo Day 6/10 22:00 JST 用 security demo segment 準備 — 両者
- [ ] Synapse Arrows Playbook v0.4 への昇格議論 (この doc を共通章に) — Cofounder

---

## 次回 review timing

- **5/12 (Week 1 終了)**: Phase 1 infra setup の進捗 review
- **5/19 (Week 2 終了)**: 法務 finalize + 機能 implementation review
- **5/26 (Week 3 終了)**: ICP-A pitch 反応 review + Phase 1 完成度判定
- **6/7 (Sprint 終了)**: pilot 1 firm 契約有無 + Online Demo Day 6/10 final prep

Phase 1 が May 中に完成しなければ、 Online Demo Day 6/10 で「security 整備中」と honest に話す。
完成すれば「**1ヶ月で会計事務所向け SaaS の security baseline 構築 — solo founder の OS architecture が効いた事例**」として narrative 化。
