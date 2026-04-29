# 4-File Structure: GOALS / STATE / DECISIONS / HEALTH

> **The minimum viable operating context for any Synapse Arrows project.**

Every Synapse Arrows project repo MUST have these four files at the root.
They are the OS substrate that makes self-similar architecture possible
(see `00-principles/self-similar-architecture.md`).

## The four files

| File | Purpose | Update cadence | Read cadence |
|---|---|---|---|
| `GOALS.md` | What we are trying to achieve, when, with what KRs | Weekly (Friday) | Every session start |
| `STATE.md` | Current production status, next actions, open questions | Daily (or per session) | Every session start |
| `DECISIONS.md` | Append-only history of why we chose X over Y | Per major decision | When touching a past decision |
| `HEALTH.json` | Machine-readable baselines + URLs that must stay 200 | When baselines shift | Daily by health-check agent |

These four are NOT optional. They are NOT a documentation team's
responsibility. They are the operating contract between human and agent.

## GOALS.md

Defines hierarchical goals at three time horizons:

```markdown
# {Project} — Goals

## North Star (reviewed every 6 months)

[1-2 sentences. The thing that, if true, means we won.]

## {Year} {Quarter} OKR (reviewed weekly, changed monthly)

**Objective**: [user-centric outcome statement]

| KR | Target | Metric |
|---|---|---|
| KR1 | [number] | [how measured] |
| KR2 | [number] | [how measured] |
| KR3 | [number] | [how measured] |

## This Week ({date range})

- [ ] [concrete deliverable 1]
- [ ] [concrete deliverable 2]
- [ ] [concrete deliverable 3]

## Trigger Rules

[If THIS happens, do THAT. Pre-commit decisions to avoid emotional pivots.]

## Guardrails

[Things we never do, regardless of pressure. ✅⚠️🚫 from BOUNDARIES.md.]
```

**Why hierarchical**: a session-level Claude needs to know "what's mine to
prioritize this week." The North Star is too far. The OKR is too broad. The
"This Week" section is the actionable list.

**Why trigger rules**: removes emotional pivot temptation. If KR1 < target by
date X, do Y. Pre-decided. No mid-flight panic.

## STATE.md

The current snapshot. Updated daily (eventually by an automated digest agent;
manually for now).

```markdown
# {Project} — Current State

Last updated: YYYY-MM-DD HH:MM JST (manual / by [author])

## Production Health Snapshot

| Surface | Status | Detail |
|---|---|---|
| {URL or service} | 🟢/🟡/🔴 | {1-line metric} |

## Squad Status

| Squad | Status | Next milestone |
|---|---|---|
| {squad name} | 🟢 ACTIVE | {what they're doing} |
| {squad name} | 🔴 not built | {when planned} |

## Today's / Recent Commits

[List last 3-7 commit SHAs with one-line description.]

## Next 3 Actions

1. [highest priority]
2. [next]
3. [next]

## Open Questions

[Things that need decision but aren't blocking. Roll daily.]

## Rollover from Previous Session

[What was in flight at last session-end. Critical for avoiding "we already
solved this" amnesia.]
```

**Why this structure**: a fresh Claude session reads STATE.md and gets 80%
of "where are we" in 30 seconds. Without it, the same session needs 30
minutes of chat-history scrolling.

## DECISIONS.md

Append-only. Every architectural or strategic decision goes here with
context, alternatives considered, reasoning, reversibility, and follow-ups.

```markdown
# {Project} — Decision Log

> Append-only. Most recent at top. Never edit past entries; correct with a
> new entry that references the old one.

---

## YYYY-MM-DD — [Short title]
CONTEXT: [why a decision was needed; what the situation was]
DECISION: [what was decided]
REASON: [why this option over alternatives]
REVERSIBILITY: High / Medium / Low
COMMITS: [git SHAs if applicable]
OPEN: [unresolved follow-ups]
```

**Why append-only**: editing past decisions destroys the audit trail. A
"supersedes" reference in a NEW entry is fine; rewriting history is not.

**Why these specific fields**: each one answers a question someone reading
6 months later will ask. CONTEXT for "what problem was this solving?" DECISION
for "what did we do?" REASON for "why not the obvious alternative?"
REVERSIBILITY for "can I undo this without breaking everything?"

## HEALTH.json

Machine-readable. Consumed by automated health-check agents.

```json
{
  "$schema_version": 1,
  "last_reviewed": "YYYY-MM-DD",
  "reviewed_by": "[name]",
  "description": "[one-paragraph explanation of what this monitors]",

  "baselines": {
    "{metric_name}": {
      "min": [number],
      "max": [number],
      "unit": "[unit]",
      "note": "[why these thresholds]"
    }
  },

  "urls_must_200": [
    "https://...",
    "https://..."
  ],

  "anomaly_routing": {
    "destination": "morning_digest",
    "urgency": {
      "critical": ["[which baselines are critical]"],
      "warning": ["..."],
      "info": ["..."]
    }
  }
}
```

**Why JSON not Markdown**: the health-check agent parses this. Humans can
still read it. Machines + humans both supported with one source.

## Session ritual using these four files

Every Claude session entering a Synapse Arrows project should:

1. **Read STATE.md first** — current state in 30 seconds
2. **Read GOALS.md** — what's important this week
3. **`recall("project-name")`** from Linksee Memory — narrative + caveats
4. **If touching a past decision area, read DECISIONS.md entry**
5. **Begin work**

Total ramp-up: 2-3 minutes. Without this ritual: 15-30 minutes of context
re-derivation per session.

## When to update each file

| Event | What to update |
|---|---|
| Session ends | STATE.md (next 3 actions, rollover note) |
| Commit made | DECISIONS.md (if architectural) + STATE.md (commits list) |
| Bug fixed | DECISIONS.md (if recurring) + the project's FIX-LOG.md |
| Friday | GOALS.md (this week section, mark complete / roll forward) |
| Monthly | GOALS.md (revisit Q-OKR alignment) |
| Threshold shifted | HEALTH.json (with note in DECISIONS.md explaining) |
| Insight discovered | Linksee Memory `remember()` (importance ≥ 0.9 if pinning) |

## When NOT to update

- Don't edit DECISIONS.md to "fix" past entries. Append a new one referencing
  the old.
- Don't make GOALS.md "aspirational" — keep it honest about what's actually
  this week.
- Don't put implementation details in GOALS.md. That's STATE.md or DECISIONS.md.
- Don't put strategic narrative in HEALTH.json. That's GOALS.md.

## Adoption checklist for a new project

```
[ ] Copy 5 templates from 05-templates/ to project root:
    [ ] GOALS.md (customize KRs)
    [ ] STATE.md (initialize health snapshot)
    [ ] DECISIONS.md (with one initial entry: "adopted 4-file structure")
    [ ] HEALTH.json (set initial baselines)
    [ ] CLAUDE.md (link to this Playbook)
    [ ] BOUNDARIES.md (define ✅⚠️🚫 for the project)
[ ] Add session ritual to project's CLAUDE.md (read STATE → GOALS → recall)
[ ] First commit message: "feat: adopt Synapse Arrows 4-file structure"
[ ] Linksee Memory: remember the adoption decision
```

Time investment: ~30 minutes for a new project, ~1-2 hours for a project
that already has scattered context to migrate in.

## Examples in the wild

- **KanseiLink** (kansei-link-mcp repo): all four present, mature.
- **AgentStars** (agent-stars repo): partial — only GOALS + STATE so far.
  May 2026 milestone: complete the four-file set.
- **ScaNavi**: PR #48 introduced CLAUDE.md + BOUNDARIES.md + ARCHITECTURE.md
  + FIX-LOG.md + REGRESSION-TESTS.md. The 4-file structure is a partial fit
  here; ScaNavi has its own variant. Will reconcile in May.

## See also

- `00-principles/infrastructure-first.md` — why this is foundational
- `00-principles/self-similar-architecture.md` — how this scales into
  embedded agents inside products
- `02-process/3-tier-boundaries.md` — the BOUNDARIES.md companion
- `05-templates/` — copy-paste starting points for each file
