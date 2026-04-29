# Infrastructure-First Principle

> **Detail iteration hell is the symptom; infrastructure absence is the disease.**

The single most important rule at Synapse Arrows. Earned through ~4 weeks of
solo-founder iteration burnout across two products.

## The pattern we paid for twice

**Linksee (old)**: 2 weeks polishing UI / chat behavior / edge cases. Each
fix interacted with prior fixes in unpredictable ways. Net progress at the
end of week 2 was sometimes negative — the product felt worse than week 1.

**ScaNavi**: same shape. The brand-parser bug was fixed three separate times
across three sessions before a structural fix (extracting to a module with
20 regression tests) finally held. Cumulative time spent: ~2 weeks.

Both episodes share a structural cause:
- No tests → each fix could silently undo earlier fixes
- No persistent memory → each session forgot what the previous decided
- No specifications → each iteration drifted from the original goal
- No boundaries → scope crept every session

When the infrastructure to remember, test, and bound is absent, **iteration
loops cost more than they produce**. You move 110 steps forward and 30
backward; net 80; over time, motivation drains.

## Industry parallel

The principle has a name: **"pave the road before driving."**

- **Stripe** spent months on internal dev tools and documentation before
  opening their public API.
- **Figma** built a WebGL rendering substrate for ~5 years before shipping
  the design tool.
- **Linear** ran on Linear (themselves) before going public.
- **Vercel** built Next.js (the tool) before scaling the hosting product.

Conversely, every story of a startup that "shipped fast" and then collapsed
chasing PMF without process-product fit (PPF) is the same shape: skip the
infrastructure tax up front, pay it tenfold later.

## The Synapse Arrows commitment

After two cycles of detail-iteration tax, we committed:

> **5月 2026 = "Infrastructure Month."**
> - No new features on existing products (only critical bug fixes)
> - 100% focus on operating-substrate construction
> - Targets: Playbook, Cowork evaluation, Anthropic-5-patterns adoption,
>   Synapse Threads MCP, Marketing Agent skills, hybrid-defense-stack ports
>
> **From June onward, every new feature MUST start from Playbook templates:**
> - 1-hour bootstrap (vs 1-2 days from scratch)
> - CLAUDE.md / BOUNDARIES.md / DECISIONS.md pre-populated
> - TDD-with-Claude (test-first)
> - Slash commands automate routine

## The third strike rule

Two cycles of detail-iteration are paid as tuition. **A third cycle is
forbidden by company doctrine.** If a future product begins to slip into
detail-iteration hell, the immediate response is:

1. Stop feature work.
2. Diagnose the missing infrastructure.
3. Build it before resuming features.

Yes, this is annoying. Yes, this delays output in the short term. The math
is unambiguous: infrastructure-first is faster overall.

## How to recognize iteration hell early

Symptoms (any one of these signals start of the pattern):

- "I fixed this last week, why is it back?"
- "Did I already write that test? Where did it go?"
- "What were we trying to do here originally?"
- A 5-line fix takes 2 hours because you have to re-derive context.
- Motivation visibly drops after 2-3 days on the same area.

Diagnosis flow:

```
Symptom present
    ↓
Is the relevant fix tested? ─── NO ──→ Add regression test FIRST.
    ↓ YES
Is the past decision documented? ── NO ──→ Write to DECISIONS.md, then fix.
    ↓ YES
Is the boundary defined? ─── NO ──→ Add to BOUNDARIES.md (✅⚠️🚫).
    ↓ YES
Was a memory entry saved? ─── NO ──→ remember() to Linksee Memory, importance ≥ 0.9.
    ↓ YES
The fix is genuinely tricky. Spend the time. Document the resolution.
```

Most "iteration hell" symptoms get resolved at one of the first three steps.

## Why this principle is solo-founder critical

With no team to absorb shock, every infrastructure gap multiplies on the
founder's mental load. Michie experienced this concretely — 4 weeks of
motivation drain, sometimes near-burnout. **Build infrastructure first =
build founder sustainability first.** This isn't a productivity hack; it's
a survival pattern.

## See also

- `00-principles/three-strike-rule.md` — the formal "no third cycle" doctrine
- `00-principles/self-similar-architecture.md` — why the same infrastructure
  should also live inside our products
- `02-process/4-file-structure.md` — the concrete implementation
- `07-learnings/2026-04-29-cofounder-session-insights.md` — origin story
