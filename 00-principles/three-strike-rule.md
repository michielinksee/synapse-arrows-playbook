# Three-Strike Rule

> **Two cycles of detail-iteration hell are paid as tuition. A third is forbidden.**

A Synapse Arrows doctrine articulated 2026-04-29 after observing the same
iteration-trap pattern recur across two products.

## The rule

Strike 1: Linksee (old) — 2 weeks burned on detail iteration, output
declined in spots. **Lesson written, paid as tuition.**

Strike 2: ScaNavi — 2 weeks burned on the same pattern (brand-parser
regressed 4 times). **Lesson reinforced, paid as tuition.**

Strike 3: forbidden by doctrine. If any future Synapse Arrows product begins
to exhibit detail-iteration symptoms (see
`00-principles/infrastructure-first.md`), the response is fixed:

1. **Stop feature work immediately.**
2. **Diagnose the missing infrastructure.**
3. **Build the infrastructure before resuming.**

This applies to:
- KanseiLink
- AgentStars
- ScaNavi (continuing)
- CardWize
- Linksee Memory
- Any new product launched 2026 onward

## Why a hard rule

Soft rules ("we should consider building infra first") collapse under deadline
pressure. Hard rules survive. The third-strike rule is hard because the
pattern is well-understood and the cost of repeating it has been measured
(two products × two weeks × motivation drain).

We do not trust our future selves to remember the lesson under stress. We
trust this written rule to enforce it.

## How to enforce

### Self-detection signals

If two or more of these appear in a single week, you are in the iteration
trap and the rule activates:

- The same bug fixed differently across multiple sessions.
- "Did I already write that test?" / "Where did this code come from?"
- Output quality not improving despite hours of work.
- A 5-line fix taking 2 hours because of context re-derivation.
- Motivation drop, increased frustration in commits.

### Activation procedure

1. Pause feature work. State clearly: "we are entering the third-strike
   protocol."
2. Open `00-principles/infrastructure-first.md` and follow its diagnosis flow.
3. Identify which infrastructure is missing for this area:
   - Tests? Add regression tests covering this bug class.
   - Memory? Write a `caveat` entry to Linksee Memory (importance ≥ 0.9).
   - Boundary? Add to BOUNDARIES.md.
   - Decision log? Append to DECISIONS.md.
   - Documentation? Add to FIX-LOG.md or ARCHITECTURE.md.
4. Build the missing infrastructure.
5. Add a "DANGER ZONE" comment at the fragile site referencing the new docs.
6. Resume feature work.

### Estimated cost vs avoided cost

- Cost of activating the protocol: 2-8 hours (write tests, write docs,
  add boundaries).
- Cost of NOT activating: ~2 weeks of repeated iteration based on
  measured precedent.

The math is unambiguous.

## Anti-pattern: "just one more fix"

The trap looks like this:

> "I know the pattern, but this bug is small. I'll just push the fix and
> add tests later."

This is the entry point to a third strike. Resist. The rule's whole purpose
is preventing this exact rationalization. If the bug is small, then writing
the test is also small, and writing it now prevents weeks of pain later.

## Public-facing position

This rule is part of why the Synapse Arrows Playbook is publicly published.
By committing to the rule in writing, in public, with a specific date and
two concrete prior strikes, we:

- Create accountability beyond Michie's personal discipline.
- Signal to potential users / partners / employees / agents that we operate
  by structural rules, not heroics.
- Allow Cofounder Claude (or any Claude session) to invoke the rule when it
  observes the symptoms — agents enforce the doctrine alongside the human.

## See also

- `00-principles/infrastructure-first.md` — the underlying principle this
  rule operationalizes
- `07-learnings/2026-04-29-cofounder-session-insights.md` — origin of the
  rule, with the two strikes documented in detail
- `02-process/4-file-structure.md` — the operational substrate that prevents
  most strikes from starting
