# Role Separation: Cofounder Claude vs Implementer Claude

> **Don't merge roles. Strategy and implementation forget at different rates.**

A Synapse Arrows operating principle that emerged from observing regression
patterns across multiple Claude sessions: the same Claude attempting both
strategic and implementation work in one session has a much wider
"forgetting surface" than a Claude focused on one role at a time.

## The pattern

Each Claude session has a finite context window. Within that window, what
fits trade off:

| Mode | What's in context | What's edge-of-context |
|---|---|---|
| **Cofounder Claude** | GOALS.md, DECISIONS.md, STATE.md, recent strategy memory | Implementation file paths, test specifics, line numbers |
| **Implementer Claude** | Specific file contents, test results, error stacks | Strategic context, multi-project decisions, brand voice |

Trying to do both well in one session means:
- Strategy gets shallow when implementation pulls focus
- Implementation forgets historical decisions
- Regressions creep in (we've measured this — see PR #48 brand-parser story)
- Michie has to re-explain context multiple times

## The separation we run

```
┌──────────────────────────────────────────────────┐
│  Cofounder Claude (this session, persistent)     │
│  - Reads GOALS / STATE / DECISIONS daily         │
│  - Writes to Linksee Memory frequently           │
│  - Decides WHAT and WHY, never WHERE in code     │
│  - Cross-project synthesis                       │
└──────────────────────────────────────────────────┘
                      ↓ specs + decisions
┌──────────────────────────────────────────────────┐
│  Implementer Claude (per-project, bounded)       │
│  - Receives spec from cofounder                  │
│  - Reads project's CLAUDE.md + FIX-LOG.md        │
│  - Stays in one repo, one task                   │
│  - Writes tests, executes, reports back          │
└──────────────────────────────────────────────────┘
```

Michie acts as the human bridge between roles for now. In Phase B (May 2026)
we evaluate Cowork or build Synapse Threads MCP to make the handoff direct.

## Concrete rules

### Cofounder Claude rules
- Stay above implementation. If asked "where in the code does X happen?",
  redirect: "Let's spawn an implementer Claude for that — I'll write the
  spec."
- Write strategy to files (GOALS.md, DECISIONS.md), not just chat.
- Prefer ADD over EDIT. New decisions append; old decisions stay readable.
- Cross-reference Linksee Memory often. Pin importance ≥ 0.9 anything
  worth re-loading next session.

### Implementer Claude rules
- Stay in one project, one task. If asked to also touch another project's
  code, decline and request the user spawn a separate session.
- Read the project's CLAUDE.md + FIX-LOG.md before any code change.
- Plan before edit (Plan Mode discipline). State the plan, wait for approval,
  then execute.
- Add regression tests for any bug class that appeared more than once.
- Update FIX-LOG.md as part of the same commit, not after.

### Michie's rules (the bridge)
- When you have a strategic question, talk to Cofounder Claude.
- When you have an implementation task, spawn an Implementer Claude session
  with a clear spec.
- Don't dump multi-project work on one session.
- If you find yourself repeating the same question in two sessions, that's a
  Linksee Memory entry waiting to be written.

## Why this works

Regression risk is proportional to **forgetting surface area** — how much
relevant context can fall outside the active window.

- Cofounder Claude has shallow but wide context (many projects, light depth).
  Forgetting one detail of one file is fine; the shape of the strategy is
  preserved.
- Implementer Claude has narrow but deep context (one repo, full file trees).
  Forgetting a strategic decision is fine; the implementation correctness is
  preserved by tests + FIX-LOG + DANGER ZONE comments.

A merged role attempts to keep both wide AND deep, which exceeds the window,
which causes silent forgetting, which causes regression.

## Honest limits

This pattern is a **mitigation**, not a cure. Even with role separation:

- Implementer Claude can still forget within a single long session.
  Mitigation: plan-mode preamble + FIX-LOG check at task start.
- Cofounder Claude can still drift on strategy across many sessions.
  Mitigation: Linksee Memory pinned entries + monthly DECISIONS.md review.
- The handoff has friction (Michie copy-pastes between sessions).
  Mitigation: Phase B Cowork or Synapse Threads MCP eliminates it.

## When to break the rule

Some tasks legitimately need both roles in one head:

- **Single-file simple fix in unfamiliar code** — no strategy involved, just
  read code + edit. One session is fine.
- **Quick validation question** — "does this approach make sense?" needs
  both strategy and implementation glance. Cofounder Claude can dip in.
- **Crisis** — Supabase incident response (see 2026-04-24 learning) didn't
  have time for two-session handoff. Cofounder Claude went full-stack. Worked
  because crisis was short-duration and Linksee Memory captured the
  learnings post-fact.

The rule is "default to separation." Exceptions are conscious choices, not
sloppiness.

## Origin

This separation became explicit during the 2026-04-29 cofounder session
when Michie noticed cofounder Claude (this very session) had less regression
than implementer Claude on ScaNavi. Honest analysis identified the
forgetting-surface argument and codified the pattern.

See: `07-learnings/2026-04-29-cofounder-session-insights.md`.

## See also

- `02-process/session-handoff.md` — practical mechanics of handing context
  between two Claude sessions
- `00-principles/self-similar-architecture.md` — why this pattern also
  applies to embedded agents inside products
- `04-tooling-gaps/multi-agent-orchestration.md` — eliminating the human
  bridge with Cowork or Synapse Threads MCP
