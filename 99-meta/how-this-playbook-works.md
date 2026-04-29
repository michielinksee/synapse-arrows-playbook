# How This Playbook Works (on itself)

A meta-document. The Playbook claims to be an operating system. This file
verifies that the Playbook itself follows its own rules.

## The Playbook is a project under its own conventions

The Synapse Arrows Playbook repo IS a Synapse Arrows project. It therefore
follows the same operating system it documents.

| Convention | How the Playbook complies |
|---|---|
| 4-file structure (GOALS / STATE / DECISIONS / HEALTH) | TBD by v1.0 (May 2026) |
| CLAUDE.md at root | ✅ present (this Playbook's session ritual) |
| Append-only DECISIONS.md | TBD by v1.0 |
| Linksee Memory entries | ✅ entity "Synapse Arrows" has multiple pinned entries |
| Public visibility | ✅ this repo is public from v0.1 |
| Versioning | ✅ this is v0.1, see README.md |

The TBD items will close in May 2026. Not having them yet is consistent
with the Playbook's own honest "tooling gaps" section — what's not done
gets listed, not hidden.

## Writing changes to the Playbook

Adding to the Playbook requires:

1. **Read first.** No new file should duplicate or contradict an existing
   one without explicit acknowledgment.
2. **One file per concept.** Don't bundle three principles into one essay.
3. **Concrete > abstract.** Every claim should be paired with a specific
   project, commit, or incident as evidence.
4. **Append-only for decisions.** If a principle changes, write a new file
   that supersedes the old one with a "supersedes:" header.
5. **Citation discipline.** When borrowing from Harper Reed / Addy Osmani /
   Anthropic / others, cite explicitly with a link.
6. **Date everything.** Every learning gets a YYYY-MM-DD prefix in
   `07-learnings/`.

## Removing or rewriting old content

The default is **don't**. Future readers may need the old content for
context. Specifically:

- Past `00-principles/` files: never remove. Supersede with a new one
  referencing the old.
- Past `07-learnings/` essays: never remove. Add a "Status" header at top if
  the conclusions are now obsolete.
- Templates in `05-templates/`: may be revised in place, with a
  "Last revised: YYYY-MM-DD" note at the top, plus a note in the relevant
  DECISIONS.md describing why.

## Reading order for new readers

If a Claude session enters the Playbook and asks "where do I start," the
canonical sequence:

1. `README.md` — what is this
2. `CLAUDE.md` — how do you operate here
3. `00-principles/infrastructure-first.md` — the foundational rule
4. `00-principles/self-similar-architecture.md` — the strategic shape
5. `02-process/4-file-structure.md` — the most-used pattern
6. `03-tools/linksee-memory.md` — the partner pattern

Total: ~30-40 minutes. Sufficient to operate competently inside any
Synapse Arrows project.

## Status of the Playbook itself (v0.1)

Built in 2026-04-29 over ~3 hours by Cofounder Claude during a 14-hour
session with Michie. v0.1 ships with:

- 4 principle files (infrastructure-first, self-similar-architecture,
  role-separation, three-strike-rule)
- 2 process files (4-file-structure, 3-tier-boundaries)
- 1 tools file (linksee-memory)
- 1 tooling-gaps file (anthropic-5-patterns-to-adopt)
- 5 templates (CLAUDE / GOALS / DECISIONS / STATE / BOUNDARIES) +
  1 JSON template (HEALTH)
- 1 learning essay (2026-04-29 cofounder session)
- 1 meta file (this one)

Files NOT yet in v0.1, planned for v1.0 (May 2026):

- `01-vision/` — North Star, product portfolio, values
- More `02-process/` — plan-mode-preamble.md, session-handoff.md
- More `03-tools/` — claude-code-best-practices.md, glama-listing.md, etc.
- More `04-tooling-gaps/` — eval-suite.md, multi-agent-orchestration.md
- `06-projects/` — pointers to each Synapse Arrows project
- `99-meta/changelog.md` — formal change history of the Playbook itself

## Why public from v0.1

Three reasons for shipping a deliberately incomplete Playbook publicly:

1. **Public commitment.** A private "I'll get to this" file slips. A public
   v0.1 with a stated v1.0 timeline doesn't.
2. **Network effects.** Other solo founders can adopt early patterns
   immediately, providing feedback that shapes v1.0.
3. **Brand positioning.** Synapse Arrows operates by methodology, not
   heroics. Public methodology is the credible signal.

## Limit of the Playbook

This Playbook describes Synapse Arrows' current operating model. It is NOT:

- A general-purpose engineering playbook (it's solo-founder agent-economy
  specific)
- Universally applicable (don't force-fit it onto, say, a hardware startup)
- Complete (gaps are intentional)
- Static (it evolves)

If you're considering adopting it, read `00-principles/` first and decide if
your context matches. If yes, the rest is high-utility. If no, take the
patterns that fit and leave the rest.
