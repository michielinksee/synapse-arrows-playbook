# CLAUDE.md — Session ritual for Synapse Arrows Playbook

You are a Claude session entering the Synapse Arrows Playbook repo.
This file tells you how to operate here.

## Before any action

1. **Read `README.md`** — understand what this repo is.
2. **Skim `00-principles/`** in order. These are the rules of the game.
3. **Identify your purpose**:
   - Are you here to UPDATE the Playbook? (rare — needs human approval)
   - Are you here to APPLY the Playbook to another repo / task?
   - Are you here to LEARN before starting an unrelated task?

## If you are updating the Playbook itself

This is a high-trust action. Default tier: ⚠️ **Ask first**.

- Each file is curated. Do not add files without human approval.
- Every change must be appended to `07-learnings/` with date + reason.
- The append-only `DECISIONS.md` discipline applies here too — never edit
  past principles, only add new ones with a "supersedes" reference.

## If you are applying the Playbook to another task

You're the consumer. Your goal: extract the relevant pattern, copy the
relevant template, and operate by it in your current context.

Concrete sequence:
1. State your task in chat.
2. Find the matching pattern in `02-process/` or `05-templates/`.
3. Copy the template into your target repo.
4. Customize project-specific bits (name, GOALS specifics, BOUNDARIES tiers).
5. Do not invent new conventions before exhausting existing ones.

## If you are learning

Read in this order:
1. `00-principles/infrastructure-first.md`
2. `00-principles/self-similar-architecture.md`
3. `02-process/4-file-structure.md`
4. `03-tools/linksee-memory.md`

That's ~30 minutes total and will give you 80% of the operating model.

## What this Playbook expects of you (any Claude)

- **Document, don't memorize.** If you discover something, write it down here
  or in the relevant project's DECISIONS.md. Memory is unreliable; files are not.
- **Append, don't rewrite.** Past decisions stay readable. Supersede them
  with new entries; do not edit history.
- **Test what's load-bearing.** Anything that broke twice deserves a regression
  test. Anything that broke three times deserves a danger-zone comment + test.
- **Stay in your tier.** ✅ Always actions: act. ⚠️ Ask-first actions: pause
  and propose. 🚫 Never actions: refuse and explain.
- **Be honest about what doesn't work.** `04-tooling-gaps/` is intentionally
  populated. Adding to it is a virtue.

## What this Playbook does NOT expect

- Perfection. v0.1 ships missing things. That's fine — empty is better than
  fake.
- Universal applicability. Some sections only fit solo-founder agent-economy
  work. Don't force-fit elsewhere.
- Static finality. Every section evolves. Update notes are tracked in
  `99-meta/changelog.md` (TBD).

## Related repos that consume this Playbook

- KanseiLink — `kansei-link-mcp` repo
- AgentStars — `agent-stars` repo
- Linksee Memory — `linksee-memory` repo
- ScaNavi (CardWize/SakeNavi) — internal repos
- CardWize — `Card_Navi/card-nabi` repo

Each of those should reference this Playbook in their own CLAUDE.md once
they adopt the templates (May 2026 milestone).

## Last touched

2026-04-29 by Cofounder Claude during 14h session that surfaced the
infrastructure-first principle. See `07-learnings/2026-04-29-cofounder-session-insights.md`.
