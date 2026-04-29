# 3-Tier Boundaries System

> **Decide once, not every time.**

Every Synapse Arrows project has a `BOUNDARIES.md` defining what agents
(human or AI) can do at three autonomy tiers. This pre-decision eliminates
the cognitive cost of judging every action mid-flight.

## The three tiers

```
✅ Always do      — execute without asking, low blast radius
⚠️  Ask first     — propose plan, wait for human OK, medium blast radius
🚫 Never do       — refuse; the action is structurally forbidden
```

## Why three tiers (not two, not five)

- **Two tiers** (do / ask): everything ambiguous becomes "ask," which floods
  the human with approvals.
- **Five tiers** (do / log / ask / escalate / never): the gradient is too
  fine; humans can't track which level each action lives in.
- **Three tiers** is the minimum that captures "obvious go," "needs human
  judgment," and "structural no." Most useful Pareto frontier.

## ✅ Always do — characteristics

The action's blast radius is bounded such that even a wrong execution
doesn't cause sustained damage.

Examples (typical for our projects):
- Run tests, lint, type-check
- Append to FIX-LOG.md or DECISIONS.md
- Refactor with full test coverage
- Update STATE.md "Next 3 Actions"
- Reply to a chat message
- Commit with passing tests + clear message

The general shape: **easy to verify, easy to revert, low blast radius**.

## ⚠️ Ask first — characteristics

The action has medium blast radius — wrong execution could waste hours, lose
data, or break experiences. Worth a 30-second human gate.

Examples:
- Add a new dependency (especially major-version bumps)
- Change a load-bearing function's signature
- Modify a public API endpoint
- Push a release / deploy to production
- Spend > $1 on a Sonnet/Opus batch
- Change a brand-voice copy
- Move a file path that other code/templates depend on

The pattern: **state your plan in chat, wait for approval, then execute.**
This is Plan Mode discipline (see `02-process/plan-mode-preamble.md`).

## 🚫 Never do — characteristics

The action's blast radius is unbounded or irreversible. Humans don't get
asked because the answer is structurally "no" — even with a yes from a
sleep-deprived human at 2am, the agent should still refuse.

Examples (typical):
- Read or echo `.env`, secrets, API keys
- Write directly to production database
- Modify Stripe / Resend / Supabase configuration via API
- Delete past entries in GOALS.md / DECISIONS.md (append-only discipline)
- Push without running tests (`--no-verify`)
- Commit code that fails the regression test suite
- Force-push to main / master
- Change Vercel environment variables programmatically
- Spend > $20 on any single batch without explicit approval

The pattern: **refuse, explain why this is in tier 🚫, suggest the right
human-approval path if applicable.**

## Tier evolution policy

Boundaries are not static. They evolve as we learn:

```
✅ → ⚠️    "Always" actions that recently caused damage move to "Ask first."
            Trigger: 1 incident attributable to that action.
            
⚠️ → ✅    "Ask first" actions that have been approved 5+ times in a row
            with no incident move to "Always."
            Trigger: explicit Michie sign-off after a review.
            
⚠️ → 🚫    "Ask first" actions that nearly caused major damage move to "Never."
            Trigger: 1 near-miss + retrospective deciding the action shouldn't
            even be available.
            
🚫 → ⚠️    Rare. Only if a "Never" action has a legitimate use case that's
            now safer due to other infrastructure (e.g., a production-safe
            wrapper got built). Requires DECISIONS.md entry explaining why
            the absolute rule is being relaxed.
            
🚫 → ✅    Never. If something was once forbidden, the lowest it can ever
            go is ⚠️.
```

This evolution should be tracked in BOUNDARIES.md itself — each tier change
gets a date + reason + linking DECISIONS.md entry.

## What lives in BOUNDARIES.md

Each project's `BOUNDARIES.md` should have three sections (see template at
`05-templates/BOUNDARIES.md.template`):

```markdown
# {Project} — Autonomy Boundaries

## ✅ Always do (no approval needed)

- [action 1]
- [action 2]
- ...

## ⚠️ Ask first (human sign-off needed)

- [action 1]
- [action 2]
- ...

## 🚫 Never do (structurally forbidden)

- [action 1]
- [action 2]
- ...

## Evolution log

| Date | Tier change | Reason | DECISIONS.md ref |
|---|---|---|---|
| YYYY-MM-DD | X → Y | ... | ... |
```

## How agents use BOUNDARIES.md

At session start (per the CLAUDE.md preamble), an agent reads BOUNDARIES.md
and internalizes the three tiers for that project. Throughout the session:

- Encountering a ✅ action: proceed.
- Encountering a ⚠️ action: state the plan, wait for human OK, then execute.
- Encountering a 🚫 action: refuse, cite the BOUNDARIES.md line, suggest the
  proper escalation path.

This converts "ambiguous judgment in the moment" into "structural lookup."
Cognitive load drops significantly for both human and agent.

## Concrete example: ScaNavi BOUNDARIES (excerpt)

```markdown
## ✅ Always do
- Run pnpm test in any package
- Append to FIX-LOG.md
- Refactor with full test coverage maintained
- Add new regression tests

## ⚠️ Ask first
- Bump a runtime dependency
- Change LLM model (Haiku → Sonnet etc.)
- Edit DANGER ZONE files (extract-recommended-brands.ts)
- Modify chat system prompts
- Spend >$1 on any single Sonnet batch

## 🚫 Never do
- Commit with failing tests
- Use --no-verify
- Push directly to main without PR
- Manually overwrite hiragana DB entries (use seed migration)
- Delete or skip regression tests
```

## Common mistakes when adopting

### Putting too much in ✅
"It's small, it should be fine" — until it isn't. If you'd be embarrassed
explaining the action to a partner or investor, it's at least ⚠️.

### Putting nothing in 🚫
The 🚫 list should not be empty. If everything is "we'll judge case-by-case,"
the system has no structural protection. There must be SOME actions that
are absolute no's.

### Letting tiers go stale
BOUNDARIES.md needs review. Schedule a monthly check during DECISIONS.md /
GOALS.md review. Promote, demote, or remove items as the project matures.

### Tier-shopping mid-action
Agent encounters a ⚠️ action, gets impatient, decides "this is really a ✅."
Refuse. The whole point of pre-decided tiers is to avoid the human / agent
in the moment from rationalizing past the rule.

## See also

- `00-principles/infrastructure-first.md` — why pre-decisions beat in-flight
  judgment
- `02-process/plan-mode-preamble.md` — the ⚠️ tier's interaction protocol
- `05-templates/BOUNDARIES.md.template` — copy-paste starter
