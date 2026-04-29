# Tooling Gaps: Anthropic's 5 Patterns We Plan to Adopt

> **The Synapse Arrows OS is process-strong, tooling-medium. These five
> Anthropic-internal patterns close most of the tooling gap.**

This file is intentionally listed — gaps are documented, not hidden. If you
discover an Anthropic-internal pattern (or any other industry pattern) we
don't have, add it here.

## Where we benchmark

Synapse Arrows ranks roughly 90% of Anthropic-internal level on **process**
(memory, structure, role separation — actually exceeding their public
documentation in some areas) but only 40-50% on **tooling automation**.

The gap is concrete and addressable. Source: 2026-04-29 research session
(see `07-learnings/2026-04-29-cofounder-session-insights.md` for full
benchmarking).

## The five patterns

### 1. Slash commands → sub-agents

Boris Cherny (Claude Code creator) drives daily workflows with custom slash
commands that spawn purpose-specific sub-agents:

- `/commit` — runs tests, formats, commits with structured message
- `/pr` — creates PR with auto-generated description
- `/simplify` — refactors a function with same tests passing
- `/verify` — runs full regression suite

For Synapse Arrows, the equivalent set:

- `/audit` — re-runs the 250-test KanseiLink audit (was manual on 4/24)
- `/release` — regen-seed → commit → push → wait for Railway → verify
- `/research` — spawns subagent for web research with summarization
- `/start-day` — runs CLAUDE.md preamble ritual + recall + STATE summary
- `/danger-check` — scans the area you're about to touch for DANGER ZONE
  comments, FIX-LOG entries, and pinned caveats

Implementation effort: 1-2 days for the initial 5 commands.
ROI: significant cognitive load reduction; routine work becomes one keystroke.

### 2. Separate git checkouts for parallel sessions

Boris runs 5 local + 5-10 web Claude sessions concurrently. To avoid branch
collisions, **each local session uses a separate git checkout** rather than
branches or worktrees.

For Synapse Arrows, this means:

```
~/projects/
├── kansei-link-mcp-main/        # this session's checkout
├── kansei-link-mcp-feature-a/   # parallel checkout for new feature
├── kansei-link-mcp-bugfix/      # parallel checkout for emergency fix
```

Each checkout is its own filesystem location with its own active session.
No `git checkout` switching. No "did I commit this on the right branch."

Effort: 1 day to set up the convention + alias scripts.
ROI: enables true parallelism, especially during launch weeks when multiple
fronts are active.

### 3. Plan Mode → auto-accept → 1-shot PR

Boris's discipline: **iterate the plan in chat until it's right, then
auto-accept the implementation in one shot.** No back-and-forth on details
mid-implementation.

This is in contrast to our current pattern: micro-iterate the
implementation, fixing small issues over many turns. The Boris pattern
front-loads the thinking.

Mechanism for Synapse Arrows:

```
1. Receive task.
2. Enter Plan Mode explicitly: "Let's plan first, no edits yet."
3. Claude proposes the full plan in chat.
4. Human + Claude refine the plan (multiple turns OK here).
5. Once plan is locked, switch to auto-accept mode.
6. Claude implements in one or two large shots.
7. Tests verify.
```

Effort: process change, no code. Re-train ourselves.
ROI: fewer total round-trips per PR; less risk of mid-implementation drift.

### 4. Screenshot debugging

Anthropic SREs feed Claude **screenshots of dashboards, error states, and
UIs** — not just logs. This is significantly faster for visual systems
(GCP console navigation, mobile app errors, Vercel build logs).

Real-world saving documented: Anthropic's data-infra team saved 20 minutes
during a Kubernetes incident by feeding the GCP UI screenshot to Claude
rather than copy-pasting log lines.

For Synapse Arrows applications:
- ScaNavi mobile bugs — screenshot the app state, paste to Claude
- Vercel deploy errors — screenshot the build log
- Supabase RLS warnings — screenshot the dashboard
- Google Play console feedback — screenshot the rejection notice

Effort: zero. Just remember to screenshot before pasting.
ROI: faster diagnosis; less context loss in copy-paste.

### 5. TDD with Claude (test-first)

Anthropic's Security Engineering team explicitly **writes tests first, then
has Claude implement**. The previous workflow ("design doc → janky code →
refactor → give up on tests") was structurally vulnerable to regression.

For Synapse Arrows, this should be the default for any code that has
appeared in a regression. PR #48's brand-parser story is exactly this
realized after-the-fact: 20 regression tests now structurally prevent
re-regression.

The pattern going forward:

```
1. Identify the bug class (any bug we've seen before).
2. Write a test that reproduces it.
3. Have Claude propose a fix.
4. Verify the test passes.
5. Commit the test + fix together.
```

For new features without prior bugs: write at least one acceptance test
before implementing. The "happy path" test forces clear thinking about the
expected behavior.

Effort: process change. Every fix takes 10-15% longer initially, ~50% less
time over the long run as regression risk drops.
ROI: structural protection; fewer 2-week iteration cycles.

## Adoption schedule (May 2026 Infrastructure Month)

| Week | Patterns to adopt |
|---|---|
| W1 (5/1-7) | #1 Slash commands (build /audit, /release, /start-day) |
| W2 (5/8-14) | #2 Separate git checkouts (set up convention) |
| W3 (5/15-21) | #3 Plan Mode 1-shot (process change, train ourselves) |
| W4 (5/22-31) | #4 Screenshot debug (habit) + #5 TDD with Claude (default) |

By end of May, Anthropic-tooling parity should be ~80%+ instead of
40-50%. Combined with our process advantages (Linksee Memory, 4-file,
role-separation), the result is a hybrid that exceeds either approach
alone.

## What we have that Anthropic doesn't (publicly)

For balance — the gap is two-way:

- **Linksee Memory** (semantic persistent memory) — Anthropic's public
  docs only show CLAUDE.md (flat text)
- **4-file structure** (GOALS / STATE / DECISIONS / HEALTH separated) —
  Anthropic uses CLAUDE.md as catch-all
- **Self-similar architecture** discipline (same OS at every scale)
- **Cofounder ↔ Implementer role separation** as explicit policy

These are publishable. The plan is to write three Zenn / Dev.to articles in
May / June introducing each, positioning Synapse Arrows as a methodology
contributor to the agent economy.

## See also

- `00-principles/infrastructure-first.md` — why these gaps matter
- `07-learnings/2026-04-29-cofounder-session-insights.md` — full benchmarking
- `06-projects/` — which projects will adopt each pattern first
