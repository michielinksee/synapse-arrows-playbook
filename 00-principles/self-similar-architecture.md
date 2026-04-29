# Self-Similar Architecture

> **One operating system, four scales.**

The operating system Synapse Arrows uses to RUN ITSELF is the same operating
system that goes inside each of our PRODUCTS to make their internal agents
self-running.

## The fractal

```
Layer 0: Synapse Arrows (the company)
   ↓ Cofounder Claude + implementer Claudes operate by this OS
   ↓
Layer 1: Products (KanseiLink, ScaNavi, AgentStars, Linksee Memory, CardWize)
   ↓ Internal agents (HOLO, DiscoverAgent, PostAgent, MemoryAgent) embed the same OS
   ↓
Layer 2: Embedded agents
   ↓ Operate by the OS — memory + tests + boundaries + decision logs
   ↓
Layer 3: End users (humans + other agents)
   ↓ Receive consistent, reliable experience because the OS is consistent
```

The OS itself has five components:

| Component | At Layer 0 (us) | At Layer 1 (product) | At Layer 2 (embedded agent) |
|---|---|---|---|
| Memory | Linksee Memory (entity-level recall) | Per-user memory tables | Per-session caveat / learning logs |
| Regression test | docs/REGRESSION-TESTS.md + pre-commit hook | Product test suite | Agent decision validation |
| Boundary | BOUNDARIES.md (✅⚠️🚫) | API rate limits, auth scopes | Per-action stake gate |
| Decision log | DECISIONS.md | service_changelog tables | agent_voice_responses + outcome logs |
| State file | STATE.md | Live dashboard / freshness endpoint | Session state per agent invocation |

Same five components. Different consumers. Same shape.

## Why this matters

### 1. Investment compounds across products

Every regression test we write strengthens the OS. Every memory pattern we
discover becomes a reusable tool. Every boundary we tighten in one product's
agent transfers as a lesson to the next.

If KanseiLink's DiscoverAgent learns "auto-accept threshold should require
≥3 outcome reports", that pattern propagates: ScaNavi's HOLO doesn't ship a
sake recommendation without 3 successful prior recommendations of the same
brand. AgentStars' PostAgent doesn't auto-publish a review without 3
moderation passes. The pattern is portable because the OS is identical.

### 2. New products bootstrap in hours, not days

A new product N+1 inherits the entire learning history of products 1..N.
Most of the work is already done because the OS pre-defines:
- The 4 files to put at the repo root
- The regression test scaffold
- The boundary tier system
- The memory recall conventions

Time to ship a new product's V0: target 1 hour. Without self-similar
architecture: 1-2 days minimum, plus the inevitable iteration tax.

### 3. Cross-product agents collaborate naturally

Because every embedded agent operates by the same OS, they speak the same
language:
- ScaNavi's HOLO can write a memory entry that KanseiLink's DiscoverAgent
  consumes (e.g., "this user's preferred SaaS for X is Y").
- AgentStars' PostAgent can read the same boundaries DiscoverAgent uses
  (preventing a moderation conflict between products).
- All of them feed evidence back to Linksee Memory for the cofounder to
  query.

This is the "agent operating layer" we're building toward — Stripe-of-payments
analog for agent operations.

### 4. Dogfooding squared

Standard dogfooding: "we use our own product." Synapse Arrows version: "the
operating system of our company IS the operating system of our products IS
the operating system of agents inside our products."

When we improve our internal Cofounder workflow, agents inside ScaNavi
automatically benefit (assuming the pattern is propagated through the
Playbook). This is unusual and powerful.

## The flywheel

> **The more users use our products, the smarter our internal correction loop
> becomes** — because every product feeds the same OS.

Mechanism:
- A user's bad sake recommendation → ScaNavi outcome log → caveat added to
  shared OS pattern library → next product's recommendation system inherits
  the lesson.
- A KanseiLink miscategorization → boundary tightened → AgentStars
  PostAgent moderation pulls from same boundary catalog.

Every correction at any layer makes every other layer better. This is the
opposite of siloed product development, where each product accumulates its
own private learnings that don't transfer.

## Strategic implication

Synapse Arrows is positioned as **an operating-system company that ships
products**, not a products company that has process discipline.

- The products are evidence the OS works.
- The OS is the durable competitive advantage.
- Publishing the Playbook publicly accelerates adoption: others use our OS
  → industry standardizes around it → our products inherit network effects.

Long-term position to occupy: agent-economy stack layer 4.

```
Layer 4: Synapse Arrows         agent operating layer (this OS)
Layer 3: Linksee Memory         agents remember
Layer 2: AgentStars             humans see agent voice
Layer 1: KanseiLink             agents discover SaaS
Layer 0: Anthropic / OpenAI     intelligence layer
```

## How to apply this principle

When designing any new feature in any product, ask:

1. Does this need MEMORY? → use the Linksee Memory pattern, even if internally.
2. Does this need TESTS? → write them in the same shape as our regression-tests.
3. Does this need BOUNDARIES? → assign tiers using the same ✅⚠️🚫 system.
4. Does it need DECISIONS logged? → use the same append-only DECISIONS.md format.
5. Does it need STATE tracking? → the same STATE.md / freshness pattern.

If yes to any, **do not invent a new pattern**. Use the existing OS at the
appropriate scale. If the existing pattern doesn't fit, that's a Playbook
update, not a project-local hack.

## See also

- `00-principles/infrastructure-first.md` — the principle that makes this possible
- `02-process/4-file-structure.md` — the concrete OS at company scale
- `04-tooling-gaps/multi-agent-orchestration.md` — how agents at different
  layers will eventually communicate (Synapse Threads MCP planned May 2026)
