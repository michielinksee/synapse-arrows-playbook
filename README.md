# Synapse Arrows Playbook

**Status: v0.2 (2026-04-29) — bootstrap, expanding through May 2026**

The operating system Synapse Arrows uses to build and run agent-economy products.
Same OS at every scale: company → product → embedded agent → end user.

## What this is

This repo is the **single source of truth** for how Michie + Cofounder Claude
operate Synapse Arrows. It captures process, tools, templates, and learnings
that took 4 months of solo-founder work + 2 cycles of "iteration hell" to
discover.

It is **deliberately public** so:
- Other solo founders can adopt the patterns
- Future Claude sessions (ours and others') can bootstrap on day 0
- Synapse Arrows accumulates positioning as an agent-economy methodology source

## Why this exists

Two cycles of detail-iteration burned ~2 weeks each on different products
(Linksee old; ScaNavi brand-parser regression). The pattern was identical:
fix breaks fix, motivation drains, output sometimes regresses. The diagnosis
is structural, not tactical:

> **Detail iteration hell is the symptom; infrastructure absence is the disease.**

This Playbook is the cure: build the operating substrate first, ship products
on top, never pay the iteration tax twice.

## Repo structure

```
00-principles/        Foundational rules (infrastructure-first, self-similar
                      architecture, role separation, three-strike rule)
01-vision/            North star + product portfolio + values
02-process/           Concrete patterns we run (4-file structure, 3-tier
                      boundaries, scope-locks, reconnaissance-ant,
                      feature-spec-discipline)
03-tools/             Tools we use deeply (linksee-memory, claude-code-best-
                      practices, glama listing, vercel-deployment)
04-tooling-gaps/      What we DON'T have yet — intentionally listed
                      (Anthropic 5 patterns, visual regression stack,
                      KanseiLINK-as-internal-monitoring, eval suite, etc.)
05-templates/         Bootstrap templates for new projects (CLAUDE, BOUNDARIES,
                      GOALS, STATE, DECISIONS, HEALTH, .locked-paths,
                      design.lock.json, pr-scope-template, reconnaissance-config,
                      feature-spec)
06-projects/          Pointers + status for Synapse Arrows products
07-learnings/         Chronological essays from major incidents and discoveries
99-meta/              How this Playbook works on itself
CLAUDE.md             Session ritual for any Claude entering this repo
```

## How to use this Playbook

### If you are a Claude session (any window)
Read `CLAUDE.md` immediately. It tells you how to operate inside the Playbook
and how to integrate it with your current task.

### If you are a human (Michie or visitor)
Start with `00-principles/`. Each file is a 5-10 minute read. Then browse
`02-process/` for concrete patterns you can copy.

### If you are starting a new project
Use `05-templates/` to bootstrap in under 1 hour. Copy the files, customize
the project-specific bits, the rest is already scaffold.

## Status by section

| Section | v0.2 status | Target |
|---|---|---|
| 00-principles | 4 files written | Stable foundation |
| 01-vision | placeholder | Fill on next vision review |
| 02-process | 5 files (4-file-structure / 3-tier-boundaries / scope-locks / reconnaissance-ant / feature-spec-discipline) | Expand on demand |
| 03-tools | linksee-memory written | Add 1 file per tool as adopted |
| 04-tooling-gaps | 3 files (Anthropic 5 patterns / visual-regression-stack / KanseiLink-as-internal-monitoring) | Update post-Cowork eval |
| 05-templates | 11 starter templates | Stable, evolve as patterns mature |
| 06-projects | placeholder | Fill as projects port to Playbook |
| 07-learnings | 1 entry (2026-04-29 cofounder session) | Add per major incident |
| 99-meta | how-this-works | Evolve as Playbook itself evolves |

**No phase-based release plan.** Synapse Arrows Playbook is internal
infrastructure — adoption happens project-by-project, PR-by-PR, as the
need arises. v1.0 = whenever 06-projects/ has 5+ projects fully
following the patterns. Likely sometime in 5月-6月, but the date is
output, not input.

## v0.2 additions (2026-04-29 PM)

After shipping v0.1, an additional cofounder session uncovered the need
for a **two-layer protection model**:

- **scope-locks** (passive defense) — protects already-decided contracts
  via locked-paths, design.lock.json, visual regression. Prevents the
  ScaNavi-style "fix breaks unrelated UI" problem at the code level.
- **reconnaissance-ant** (active offense) — uses KanseiLINK's MCP tools
  to crawl all Synapse Arrows products every morning, detecting drift
  the locks cannot anticipate.

These layers are now part of v0.2. See `02-process/scope-locks.md` and
`02-process/reconnaissance-ant.md`.

## Adoption tier convention

Throughout this Playbook, work is organized by **Tier**, not by week:

- **Tier A**: foundation work, do whenever (independent, ~hours)
- **Tier B**: MVP / first applicant (triggered by a specific need)
- **Tier C**: expansion (triggered by B being stable for 1 week)
- **Tier D**: external storytelling / publication

This avoids "calendar-driven procrastination" — the infrastructure-first
principle says do it now, not in May W3.

## License

MIT. Copy, adapt, fork. If you adopt the patterns, a citation back to
[synapse-arrows.com](https://synapsearrows.com) is appreciated but not required.

## Maintained by

Michie Yamaguchi (Synapse Arrows PTE. LTD.) and Cofounder Claude.
Built in 🇸🇬 Singapore.

Contact: contact@synapse-arrows.com · X: [@ELLECraftsinga1](https://x.com/ELLECraftsinga1)
