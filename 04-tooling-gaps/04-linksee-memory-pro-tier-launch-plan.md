# Linksee Memory — Pro Tier Launch Plan (May Sprint)

> Status: planning, 2026-05-07 起案 → **5/7 PM May Sprint mode** (4週 → 1-2週へ圧縮)
> Target launch: **2026-05-19 by EOW (Week 2)** — その後 5月後半 = 拡散 phase
> Owner: Michie + Cofounder Claude (戦略 / 実装監督) + Implementer Claude (実装)
> Predecessors: [scope-locks](../02-process/scope-locks.md), [feature-spec-discipline](../02-process/feature-spec-discipline.md)
> Companions: [05-kansei-link-finance-vertical-pivot](./05-kansei-link-finance-vertical-pivot.md), [06-tokyo-conference-strategy](./06-tokyo-conference-strategy.md), [07-kansei-link-cockpit-security-posture](./07-kansei-link-cockpit-security-posture.md)

## 🔴 2026-05-07 PM 重要更新: May Sprint mode

Michie 確認 (5/7): 「計画が遅すぎる。 1-2 日で実装してそこから拡散、 全部 5 月で終わらせる」

→ 当初 4-week sprint は **2-week implement + 2-week marketing** に圧縮。
→ Linksee Memory Pro tier は **5/19 (Week 2 EOW) 完成** → **5/20-5/31 拡散 phase**。
→ Tokyo Conference 6/10 は launch ではなく **"拡散 phase の peak moment"** に再定義。

### May Sprint timeline (圧縮版)

| Week | 期間 | 主任務 | 副任務 | 状況 |
|---|---|---|---|---|
| **Week 1** | 5/7 - 5/12 | ~~Resources + Sampling 実装~~ → **Five Blocks 全実装** | LP wireframe + Stripe account | ✅ **5/7 中に完了** |
| **Week 2** | 5/13 - 5/19 | LP 公開 / waitlist 開始 / Pro tier API gate | bilingual UI / Stripe webhook | 🔵 進行中 |
| **Week 3** | 5/20 - 5/26 | **拡散 phase**: X thread / Zenn 第3弾 / Reddit / HN Show HN | Conversion optimization | 🟡 待機 |
| **Week 4** | 5/27 - 5/31 | **拡散 + waitlist closing 100 人 hit** | Online Demo Day prep | 🟡 待機 |
| **Bonus** | 6/1 - 6/9 | Pro tier paid sign-up open | Online Demo Day rehearsal | 🟡 待機 |
| **Peak** | 6/10 | Online Demo Day 22:00 JST (Tokyo Conf 終了直後) | YouTube Live + X Spaces | 🟡 待機 |

### 🟢 Week 1 (5/7) — 完了サマリ

May Sprint Day 1 (= 5/7) で **想定 5-7 日分の実装を 1 セッションで完走**:

| Block | Surface | Status |
|---|---|---|
| Tools | 8 tools (signature 不変、 backward compat) | ✅ unchanged |
| **Resources** | `memory://stats` / `memory://hot` / `memory://recent` / `memory://caveats` + 3 templates | ✅ NEW |
| **Prompts** | 5 templates (`summarize-session` / `extract-caveats` / `weekly-consolidation` / `recall-and-write` / `entity-handoff`) | ✅ NEW |
| **Sampling** (opt-in) | `consolidate use_llm:true` で client LLM に再要約依頼 | ✅ NEW |
| **Roots** (opt-in) | `recall_file scope_to_roots:true` で client root 内の path に絞る | ✅ NEW |
| **Elicitation** (opt-in, newer) | `forget interactive:true memory_id:N` で user 確認 | ✅ NEW |

実績:
- PR #1 merge (squash → commit `78999b5`)
- README v0.3.0 セクション (commit `e00542e`)
- CI green 1発 pass (Build + handshake)
- npm published `latest = 0.3.0` (https://www.npmjs.com/package/linksee-memory/v/0.3.0)
- git tag `v0.3.0` pushed
- smoke v0.2 backward-compat 全 pass
- smoke v0.3.0 全 pass (Resources + Prompts + tool flag back-compat)
- Linksee Memory caveat pin (memory_id 114623) — npm publish 罠 3 つ + 再現手順

→ Week 2 タスクに前倒し着手可能。 Week 1 残り (5/8-5/12) は **LP wireframe + Stripe account + Zenn 第3弾 draft 着手** に充てる。

### Week 2 plan (5/13 - 5/19) — 前倒し着手で 5/12 までに完成目標

| Day | Task | Owner |
|---|---|---|
| 5/8 木 | Zenn 第2弾 publish (Glama 5 traps) + X thread → reach 観測 | Michie |
| 5/8 木 | Pro tier LP wireframe (Vercel + Tailwind) draft | Cofounder |
| 5/9 金 | Stripe account 開設 + Pro tier $5/$10/$50 product 作成 | Michie + Cofounder |
| 5/10 土 | Dev.to 英語版 publish (Glama 5 traps EN) | Cofounder draft → Michie review |
| 5/11 日 | Pro tier API gate 実装 (license check via Cloudflare Worker) | Cofounder |
| 5/12 月 | LP 公開 + waitlist signup form ライブ | Cofounder |
| 5/13-5/15 | bilingual UI (JP/EN) 切替 + Stripe webhook 接続 | Cofounder |
| 5/16-5/19 | Zenn 第3弾 draft (v0.3.0 Five Blocks 事例 = 業界先行 1% narrative) | Cofounder draft → Michie review |

## Why now (この doc が存在する理由)

2026-05-06 時点の状態:

- npm DL: 1,903 (3週間 / launch 後)
- GitHub stars: 3
- Glama Score: A · A · B (Maintenance "6か月" 縛りが残課題)
- Tools 8個実装済 (recall, remember, list_entities, forget, consolidate, recall_file, read_smart, update_memory)
- **MCP の Prompts / Resources / Sampling / Roots 未実装**
- **Pro tier / paid 機能 0** — bootstrap free OSS のまま

bootstrap で月 $10K MRR が "勝ち" の definition として合意済 (Cofounder 議論 2026-05-07)。ここから逆算すると **Pro tier 100 paying users × $10/mo = $1K MRR** が即時 milestone、その10倍が validation。

「**営業をするときがきた**」 (Michie 2026-05-07) — landing page + Stripe + waitlist 募集 を 4週間で stand up する。

## Hypothesis — 何が paying user を生むか

### ICP 仮説 (3つ、validate 中)

| ICP | Pain | Linksee Memory が解く value | Pro tier に払う理由 |
|---|---|---|---|
| **A. Solo developer** (Cursor / Claude Code daily user) | session ごとの記憶喪失で同じ説明を繰り返す | local-first 6-layer 永続記憶 | cross-device sync が欲しい (会社 PC / 自宅 / 出張) |
| **B. Engineering team lead** (5-20 人 dev team) | チーム内で同じ debug / 同じ意思決定を別人が再発見する | shared team memory + caveat 永続 | 「過去の教訓を team 全員で共有」したい |
| **C. AI agent power user** (複数 LLM + tool 横断、prompt engineer) | tool 越えた context 維持が困難 | entity 単位の cross-tool memory | 自分の workflow 全部の "外部脳" 必要 |

→ **A が waitlist 数稼ぎ、B が単価高、C が evangelist** という分業期待。

### 価格仮説 (検証対象)

| Tier | Price | Gated features | 期待 conversion |
|---|---|---|---|
| **Free (OSS)** | $0 | 全 local 機能。 npm install で即動く | infinite (現状の path) |
| **Pro** | $5/mo or $10/mo | cloud sync (cross-device), 大容量 (>10K memories), priority models, 日英 UI | DL 数の 5% (Mem0 と同 cohort) |
| **Team** | $50/seat/mo (5+ seats) | shared team memory + caveat 共有 + audit log | 数社 pilot (B2B 営業 cycle) |
| **Enterprise** | custom (推定 $5K-30K/mo) | SSO + on-premise + SLA + 特注 | Tokyo Conference 後に着手 |

→ Pro $5 か $10 か は landing page A/B で確定。Team / Enterprise は後段。

### Conversion KPI (4-week sprint 終了時点)

| Metric | Target | Stretch |
|---|---|---|
| Waitlist signup | 100人 | 300人 |
| Waitlist → Pro conversion | 30% | 50% |
| 初月 paying user | 30人 | 100人 |
| 初月 MRR | $150 | $500 |

これが達成できれば **市場仮説 validation 成立**、 6月以降 Team tier B2B 営業に着手。

## 実装プラン (4-week sprint)

### Week 1 (5月W2 — 5/12-5/18): MCP 5 blocks の **Resources** 実装

**Goal**: entity を MCP Resource URI で公開し、 client が memory 全体を RAG できるようにする。

**Deliverables**:
- `linksee-memory://entity/{entity_name}` URI scheme 設計
- `registerResource` を `dist/mcp/server.ts` に実装
- 各 entity の memory 全文 + metadata を resource として返す
- streaming 対応 (large memory entity 用)
- `Resource` schema を test (`@modelcontextprotocol/inspector` で確認)

**Success criteria**:
- VS Code / Claude Desktop で resource browser から entity 一覧見える
- `linksee-memory://entity/Synapse Arrows` を選択 → 該当 memory 全部表示

**Linked spec**: [feature-spec-discipline](../02-process/feature-spec-discipline.md)

### Week 2 (5月W3 — 5/19-5/25): **Sampling + Server-side Agent Loop**

**Goal**: `consolidate` tool を Async Task + Sampling 経由の自律ループに進化。

**Deliverables**:
- `consolidate` tool を **Async Task primitive** に書き換え
- Task state machine (working / input_required / completed / failed)
- 内部 Sampling chain:
  1. cold な (heat < 0.3) memory を fetch
  2. Sampling: 「これらを 6-layer のどれに分類すべきか」 client AI に依頼
  3. 重複検出 (`Sampling`)
  4. 統合候補生成 (`Sampling`)
- result は `recall` で再取得可能な形で記録

**Why critical**:
これがないと 「自動進化する記憶」 brand が成立しない。 Mem0 との差別化軸 = "structure + autonomy" の autonomy 部分。

**Success criteria**:
- VS Code で `consolidate` を起動 → progress 表示 → 完了通知
- 結果として cold memory が consolidated entry に変換されている
- token cost: server 側 0 (client AI が処理)

### Week 3 (5月W4 — 5/26-6/1): **Elicitation + 日英 bilingual**

**Goal 1 (Elicitation)**: `consolidate` の途中で「これら統合する?」を user に out-of-band 確認。

**Deliverables**:
- URL mode elicitation の実装
- web UI (linksee.com 内) で承認 / 拒否
- 結果が server に返る

**Goal 2 (Bilingual)**:
- `recall` / `remember` の **出力言語切替** (env: `LINKSEE_LANG=en|ja`)
- `consolidate` の Sampling prompt も bilingual 対応
- README + SKILL.md の英語訳追加

**Why**: Pro tier 営業を **global** 視野に展開するため。日本語のみ → 英語含む = TAM が10x。

**Success criteria**:
- `LINKSEE_LANG=en` で全 tool 出力が英語
- `LINKSEE_LANG=ja` で日本語
- web UI も切替可能

### Week 4 (6月W1 — 6/2-6/8): **Pro tier landing page + Stripe + waitlist**

**Goal**: 払う人を集める。

**Deliverables**:

#### Landing page on linksee.com (新規 page or section)

```
/pro                       (英語版)
/pro/ja                    (日本語版)
```

Structure:
1. **Hero**: "AI agents that remember. Forever."
   - sub: "Local-first 6-layer memory for Claude Code, Cursor, ChatGPT — now with cloud sync."
   - CTA: "Join the waitlist"
2. **Pain story**: "Your AI is dumb because it forgets" (data: 88% of devs report repeating themselves to AI)
3. **Demo video / GIF**: recall → consolidate → cross-device sync
4. **Features comparison table**: Free vs Pro vs Team
5. **Pricing**: $5/mo or $10/mo (A/B test)
6. **Waitlist form**: email + use case (radio: solo / team / agent power user)
7. **Testimonials placeholder**: 取得後に挿入
8. **FAQ**: privacy / open source license / cancel anytime / data export

#### Stripe integration

- Stripe Checkout (一番速い)
- waitlist signup → email collected → 「launch 時に notify」flow
- `published: false` 状態で landing page は available
- launch 時に Stripe checkout enable

#### Waitlist 募集 channel

| Channel | Audience | 期待 signup |
|---|---|---|
| **Zenn 第2弾記事 末尾 CTA** | 日本 dev | 30-50人 |
| **Dev.to 英語版** | global dev | 30-50人 |
| **X 日英 thread** | 既存フォロワー + 拡散 | 30-100人 |
| **Show HN (Hacker News)** | global early adopter | 50-200人 (当たり次第) |
| **Reddit r/ClaudeAI** | Claude power user | 20-50人 (karma 制約あり) |
| **MCP Discord** | MCP 開発者 | 10-30人 |
| **Tokyo Conference 6/10** | Japan dev / engineers | 50-100人 (会場で) |

**Total target**: 220-580人 → 100人達成は十分現実的。

## Conversion 戦略

### Waitlist → Paying ユーザーへの brief 期待

waitlist signup 後のシーケンス:

```
Day 0: 即時 confirmation メール
       「ありがとうございます。launch 通知を送ります。」
Day 7: 進捗 update メール
       「Pro tier 機能の demo video です」 (5 min)
       「使用例: cross-device で開発中のプロジェクト memory を共有」
Day 14: launch 予告
       「6/10 launch 予定です。waitlist の方は最初の30日無料」
Day Launch: launch メール
       「Pro tier がオープンしました。30日無料で試せます。」
       「→ Stripe checkout link」
Day Launch+7: 利用 update
       「現在 cross-device で X 個の memory を共有中」
Day Launch+30: convert メール
       「無料期間が終わります。継続するか?」
```

→ **30日 free trial** は conversion を上げる定番手法。

### A/B 検証項目 (waitlist 段階)

| 項目 | A | B | metric |
|---|---|---|---|
| Pricing | $5/mo | $10/mo | signup rate |
| Headline | "AI agents that remember" | "Stop explaining the same bug to AI" | click-through |
| ICP focus | Solo dev | Team / company | qualified signup% |
| 30日 trial | あり | なし | conversion rate |

## Linked Synapse Arrows assets

- Existing repo: https://github.com/michielinksee/linksee-memory (npm `linksee-memory`)
- Website: linksee.com (existing infrastructure, Stripe 既存連携)
- Zenn series:
  - 第1弾: [Linksee Memory を作った話 (4/22)](https://zenn.dev/michielinksee)
  - 第2弾: [あなたの MCP server、実は Glama listing で3週間止まる (5/8 公開予定)](../../KanseiLINK-zenn-contents-link)
  - 第3弾: 「5 blocks 実装事例 + Pro tier 発表」 (6/9 公開予定、Tokyo Conf 直前)
- Linksee Memory caveat #86417 (Glama mechanics)
- Linksee Memory caveat #92572 (Vercel git-author auth)
- Linksee Memory caveat #99005 (npm token rotation)

## DECISIONS log (このプランの判断)

### 2026-05-07 — Pro tier launch decision

**CONTEXT**:
1,903 DL accumulated, 3 stars only. Cofounder Claude による strategic 評価 (2026-05-07) で:
- Linksee Memory niche A path (= local-first + 6-layer 寡占): 70% confidence
- Pro tier 検証なしでは、 niche claim が assumption のまま
- Mem0 が $24M raise ($24M = 4-people lean infra 投資) で同 vector 攻めている

**DECISION**:
- 4週間 sprint で Pro tier launch
- 6/8 Tokyo Conference 直前 launch
- Pricing $5 vs $10/mo を waitlist で A/B
- 100人 waitlist + 30人 paying = 初期検証 milestone

**REASON**:
- "営業をするときがきた" (Michie) — community building だけでは検証できない
- Mem0 と異なる positioning (local-first + structure) を市場に試せる時期
- 4週間 sprint なら Tokyo conf 物語に組込可能 ("launched 2 days before this conference")

**REVERSIBILITY**:
High — Pro tier がうまくいかなければ landing page を pause すれば戻せる
OSS は continue 提供

**OPEN QUESTIONS**:
- ICP A / B / C のどれが最も convert するか
- $5 vs $10 で signup 数が大きく変わるか
- Team tier ($50/seat) の B2B 営業はいつ着手するか
- Enterprise tier (SSO/SLA) は Tokyo Conf で 1社 anchor 取れた後

## Anti-patterns to avoid

- **Pro tier 機能を free に乗せる衝動** → free vs paid の境界曖昧化、誰も払わない
- **Stripe 統合を complex にする** → checkout は1 click、annual 割引等は phase 2
- **launch 時に too many features 押し込む** → 1-2 features (cloud sync が main) に絞り込む
- **6月 launch の遅延** → Tokyo Conference 6/10 とのリンクが切れる、その効果消える

## Next actions (this week)

- [ ] 5/12 までに Resources 実装 spec (`docs/specs/resources.md`) 完成
- [ ] 5/19 までに Sampling chain の prompt design
- [ ] 5/26 までに Elicitation web UI mockup
- [ ] 6/2 までに linksee.com /pro page wireframe
- [ ] 6/8 までに waitlist 公開
