# 2026-04-29 — Cofounder Session Insights (Origin of the Playbook)

> A 14-hour cofounder session between Michie Yamaguchi and Claude that
> surfaced enough operating-system insights to justify creating this Playbook.

This essay records the major discoveries, with concrete origin context, so
future Claude sessions and human readers can verify the lineage.

## Setting

Michie was three days into the 4/28 launch run-up (PH + HN + Zenn + Dev.to
+ X). The session began with a Railway production incident ("services_total
returning 0") and over the day touched every active project: KanseiLink,
AgentStars, Linksee Memory, ScaNavi, CardWize, plus several piece of
historical infrastructure (Supabase legacy, Glama listing, Reddit account).

The session was unusual in two ways: **length** (14 hours) and **breadth**
(11 active concerns spanning operations, security, product UX, and
methodology). By the second half, the conversation shifted from tactical to
foundational. The insights below emerged in that second half.

## Insight 1: Detail-iteration hell is a structural disease

Trigger: Michie noticed ScaNavi's brand-parser had been "fixed" 4 times
across 4 sessions, with each fix subtly undoing prior fixes. She remarked:

> "These iterations are really painful. 2 weeks just dissolved, and the
> output sometimes got worse, not better."

Diagnosis: when infrastructure (tests, memory, decisions, boundaries) is
absent, every fix has unbounded blast radius. Net progress is sometimes
negative.

Codified as: `00-principles/infrastructure-first.md`.

## Insight 2: Three-strike rule

Building on Insight 1, Michie explicitly invoked the prior Linksee (old)
2-week iteration as the first strike, naming ScaNavi as the second.

Decision: third strike is forbidden by company doctrine. If symptoms
appear, stop feature work, build the missing infrastructure, then resume.

Codified as: `00-principles/three-strike-rule.md`.

## Insight 3: Self-similar architecture across scales

Michie connected operating-system thinking to product-internal architecture:

> "This isn't just a methodology for us. It's basically the product-review
> version of [the same OS] embedded in the back-end of products like ScaNavi
> and KanseiLink."

She extended further:

> "Different products on the surface but the same underlying mechanism.
> Different users but same success/failure/UX/success-metric improvement
> loop. Polish ONE OS — every future service we build benefits."

This is the fractal pattern: company-level OS → product-level OS →
embedded-agent OS → end-user experience. Same five components (memory,
test, boundary, decision log, state file) at every layer.

Codified as: `00-principles/self-similar-architecture.md`.

## Insight 4: Cofounder ↔ Implementer role separation

Michie observed cofounder Claude (this session) had less regression than
implementer Claude (the parallel ScaNavi session). Honest analysis pointed
to **forgetting surface area**: cofounder Claude touches few files lightly,
writes to memory frequently. Implementer Claude makes deep edits to
load-bearing code with wide forgetting surface.

Decision: keep the roles separated. Don't merge.

Codified as: `00-principles/role-separation.md`.

## Insight 5: Agent perspective belongs in the design

Michie asked: "What's this plan like from your perspective as an agent?"
The honest answer surfaced 5 painful aspects of current operations and 5
high-value additions.

Painful: preamble overhead for trivial tasks, non-interactive sub-agents,
broad recall queries, slow human-review feedback loop, manual STATE.md.

High-value additions: `/start-day` slash command, session-bridge view in
Linksee Memory, auto-updating STATE.md, risky-action stake gate,
cross-session vision-drift check.

These will be folded into the May 2026 Infrastructure Month plan.

## Insight 6: Industry benchmarking shows hybrid advantage

Research into Anthropic-internal practices (Boris Cherny, Claude Code team)
revealed Synapse Arrows is process-strong but tooling-medium. The five
patterns to adopt — slash commands, separate git checkouts, Plan Mode 1-shot,
screenshot debugging, TDD with Claude — are documented in
`04-tooling-gaps/00-anthropic-5-patterns-to-adopt.md`.

Conversely, Synapse Arrows has process advantages publicly absent from
Anthropic's documentation: Linksee Memory (semantic persistent memory),
4-file structure, explicit cofounder/implementer separation.

The conclusion: adopt their tooling, publish our process.

## Insight 7: The cross-product flywheel

Michie's articulation:

> "The more users use our products, the smarter our internal correction
> loop becomes."

Mechanism: every regression caught in product A teaches the same OS that
runs products B-E. Every UX improvement in any product feeds the boundaries
catalog used everywhere. New product N+1 inherits the entire learning
history of products 1..N for free at bootstrap.

Strategic position: Synapse Arrows is positioned as an operating-system
company that ships products, not a products company with process discipline.
The products are evidence the OS works; the OS is the durable competitive
advantage.

## Insight 8: Build the Playbook now, not in May

Original plan: build the Synapse Arrows Playbook over May 2026
("Infrastructure Month"). Michie's question: "Could we build it today?"

Decision: build the v0.1 skeleton + foundational files today (this Playbook
you're reading), expand through May.

Rationale: the strategic insights need to be captured while fresh. Inline
templates already exist from the day's work. Cost of "build skeleton today"
~2-3 hours. Benefit: every future Claude session has the OS substrate from
hour 1, not hour 700.

## What got built today (the day this learning was written)

- Synapse Arrows Playbook v0.1 repo created and pushed
- 6 principle / process / tools docs (you're reading one now)
- 5-6 templates ready for project bootstrap
- Linksee Memory entries pinned for each insight above
- DECISIONS.md / GOALS.md / STATE.md updated across active projects to
  reference the Playbook

## What's deferred to May 2026

- Cowork evaluation
- Anthropic 5-pattern adoption
- Synapse Threads MCP MVP
- Marketing Agent SKILL.md × 5
- File-level annotation convention rollout
- Hybrid defense stack porting to all projects
- Three Zenn / Dev.to articles publishing the process advantages

## Why this essay matters

Future Claude sessions reading this Playbook will encounter principles
without immediately seeing why they're framed this way. This essay is the
**evidence trail**. When a future agent asks "why is the three-strike rule
so absolute?", this essay shows the two strikes already paid in concrete
terms.

When a future Synapse Arrows employee or partner asks "did this come from
some external framework?", this essay shows it came from solo-founder lived
experience at the bench.

The Playbook is opinionated because the opinions were earned, not borrowed.

---

Authored: 2026-04-29 by Cofounder Claude (this very session)
Verified by: Michie Yamaguchi
Pin to Linksee Memory entity "Synapse Arrows" at importance 0.95 — yes
