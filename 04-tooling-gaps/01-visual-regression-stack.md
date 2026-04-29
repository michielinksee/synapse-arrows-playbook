# Visual Regression Stack — Tooling Decision

> Status: gap as of v0.2 (2026-04-29). Adoption: 5月W3.
>
> Synapse Arrows の UI重視プロダクト（ScaNavi / AgentStars / CardWize）は
> [scope-locks](../02-process/scope-locks.md) の Layer 5 が必須。本書は
> ツール選定の比較と暫定決定。

## Why this gap exists

scope-locks Layer 1〜4 は「明示的に凍結したものを守る」までしかできない。
画面の **ピクセル単位の劣化** は、人間が目視で発見するまで通る。

これは特に Claude が頻繁にCSSを触るプロジェクトで顕著で、ScaNavi で実際に
発生した（チャット改善PRに伴う UI のじわじわ揺り戻し）。

## Options compared

| ツール | 動作モデル | 月額（5プロダクト） | 既存スタック適合 | 学習コスト |
|---|---|---|---|---|
| **Playwright Snapshot** | self-host, repo内 baseline | $0（CI分のみ） | ✅ Next.js / RN web | 低（Playwrightすでに使う場合） |
| **Chromatic** | hosted, Storybook連携 | $149+/mo | ✅ Storybook前提 | 中 |
| **Percy (BrowserStack)** | hosted, multi-browser | $149+/mo | ✅ どれでも | 中 |
| **reg-suit** | self-host, S3 baseline | $0（S3分のみ） | ✅ どれでも | 中高 |
| **手動 + KanseiLINK take_snapshot** | reconnaissance ant統合 | KanseiLINK運用コスト | ✅ Synapse Arrows特有 | 低（既存資産） |

## Recommendation

**Playwright Snapshot を CI 層に、KanseiLINK take_snapshot を本番監視層に**。

理由:

1. Playwright Snapshot は **PR時点で止める**（scope-locks層5）
2. KanseiLINK take_snapshot は **本番で毎朝検出**（reconnaissance-ant）
3. 両者は役割が違うので競合しない
4. Chromatic/Percy は月額が積み上がる（5プロダクト × $149+ = $750+/mo）。
   solo-founder段階では不適
5. reg-suit は self-host のメンテコストが大きい

## Adoption schedule

### W3 (5月) — 各プロダクトに5本ずつ

ScaNavi（最初の適用先）:
- [ ] `tests/visual/chat-empty.spec.ts`
- [ ] `tests/visual/chat-with-recommendation.spec.ts`
- [ ] `tests/visual/chat-editable-chip.spec.ts`
- [ ] `tests/visual/chat-error-state.spec.ts`
- [ ] `tests/visual/chat-empty-result.spec.ts`

AgentStars / CardWize / KanseiLink admin / Linksee Memory CLI も同様に。

### W4 — CI integration

- [ ] `.github/workflows/visual-regression.yml`
- [ ] Baseline 更新フロー（PR comment で `/update-baseline`）
- [ ] 失敗時の Slack 通知

## Concrete usage example

```ts
// tests/visual/chat.spec.ts
import { test, expect } from '@playwright/test';

test.describe('ScaNavi chat — visual lock', () => {
  test('empty state renders identical', async ({ page }) => {
    await page.goto('/chat');
    await expect(page).toHaveScreenshot('chat-empty.png', {
      maxDiffPixelRatio: 0.01,
    });
  });

  test('recommendation result renders identical', async ({ page }) => {
    await page.goto('/chat');
    await page.fill('[data-testid=chat-input]', '辛口の重いの');
    await page.click('[data-testid=chat-submit]');
    await page.waitForSelector('[data-testid=recommendation-card]');
    await expect(page).toHaveScreenshot('chat-recommendation.png', {
      maxDiffPixelRatio: 0.02, // 推薦内容は若干揺れがあるので緩め
    });
  });
});
```

## Caveats

- **Font rendering の OS差**: macOS / Linux CI の rendering が異なる。
  Docker base image を CI と統一すること（`mcr.microsoft.com/playwright`）
- **動的コンテンツ**: 日付、ランダム要素は mock or hide
- **アニメーション**: `page.evaluate(() => document.body.style.animation = 'none')`
- **Retina/scale factor**: `viewport.deviceScaleFactor` 統一

## Connection to other layers

- [scope-locks.md](../02-process/scope-locks.md) Layer 5 の実装
- [reconnaissance-ant.md](../02-process/reconnaissance-ant.md) と相補（CI vs 本番）
- [`02-kansei-link-as-internal-monitoring.md`](./02-kansei-link-as-internal-monitoring.md)
  と相補（CI vs cross-product）
