# Linksee Memory: Persistent Semantic Memory for Agents

> **The substrate that makes "previous session decided X" actually retrievable.**

Linksee Memory is Synapse Arrows' open-source MCP server providing
local-first, semantically-organized persistent memory for AI agents. Within
the Synapse Arrows OS, it occupies the third layer of the agent-economy
stack and is the primary tool that prevents Claude sessions from amnesia.

Repo: https://github.com/michielinksee/linksee-memory

## Why this exists

Without persistent memory:
- Every Claude session starts cold
- Decisions made yesterday are forgotten today
- The same bug gets diagnosed three times (the iteration-hell pattern)
- Strategic context is re-derived from chat scrolling each session

CLAUDE.md helps with project-level state but is project-scoped and flat.
For cross-project, cross-session, semantically-tagged memory with importance
weighting and forget-protection, you need a database with a real schema.

That's Linksee Memory.

## Core concepts

### Six memory layers

Every memory is tagged with one of six layers, each capturing a different
kind of knowledge:

| Layer | What it stores | Forget-protected? |
|---|---|---|
| `goal` | Why the entity exists / what it's pointed at | No (LRU forgets if cold) |
| `context` | Current situation / why-this-now | No |
| `emotion` | User mood, relationship dynamics, founder state | No |
| `implementation` | How something works / past success or failure | No |
| `caveat` | Pain lessons — never do this again | **Yes** (forget-protected by default) |
| `learning` | Growth log / new realizations | No |

The asymmetry — only `caveat` is forget-protected — is intentional. Painful
lessons cost more than they're worth to forget. Implementation details age
out naturally.

### Entities

Memories attach to entities. Each memory has:
- `entity_name` — human-readable
- `entity_kind` — `person | company | project | concept | file | other`
- `entity_key` — optional canonical key (email, domain, file path)

Entity-level recall is the primary access pattern: `recall("KanseiLink")`
returns memories about KanseiLink across all layers.

### Importance and forgetting

Each memory has `importance: 0.0-1.0`:
- `0.9+` pins the memory — survives forgetting passes
- `0.5-0.89` normal weighting
- `<0.5` likely to be forgotten in consolidation

Run `consolidate()` periodically to dedupe and prune. Pinned memories survive.

## Synapse Arrows usage patterns

### Pattern 1: Entity caveats (most common)

When a session discovers something painful, save it as a caveat:

```typescript
remember({
  entity_name: "ScaNavi",
  entity_kind: "project",
  layer: "caveat",
  importance: 0.95,
  content: "Brand parser regressed 4 times. extract-recommended-brands.ts is LOAD-BEARING. __tests__/ has 20 regression tests, do not remove. See FIX-LOG.md PR #48."
})
```

Future Claude sessions querying `recall("ScaNavi")` see this immediately.

### Pattern 2: Per-person preferences

```typescript
remember({
  entity_name: "Michie",
  entity_kind: "person",
  layer: "context",
  importance: 0.85,
  content: "Bilingual founder; prefers data-first decisions; treats agents as peers; has experienced 2 detail-iteration cycles."
})
```

### Pattern 3: Cross-project goals

```typescript
remember({
  entity_name: "Synapse Arrows",
  entity_kind: "company",
  layer: "goal",
  importance: 0.95,
  content: "Position as agent operating-system layer..."
})
```

### Pattern 4: File-level annotations

```typescript
remember({
  entity_name: "C:/Users/HP/scanavi/.../extract-recommended-brands.ts",
  entity_kind: "file",
  layer: "caveat",
  importance: 0.9,
  content: "Past 4 regressions. Don't remove tests. Don't add new substring matchers without TDD."
})
```

Then `recall_file(path)` returns annotations specific to that file. This is
the foundation of cross-window file-annotation (any Claude in any tool sees
the same annotations).

## Conventions for Synapse Arrows projects

### Importance levels

| Level | When to use |
|---|---|
| 0.95+ | Foundational principle, major caveat that must never forget |
| 0.85-0.94 | Important context worth pinning |
| 0.5-0.84 | Routine knowledge |
| <0.5 | Disposable, will be forgotten |

### Layer choice cheat-sheet

- "Why are we doing X?" → `goal`
- "What's the current situation around X?" → `context`
- "How is X person feeling / trending?" → `emotion`
- "How does X work / what was tried?" → `implementation`
- "Don't do X / X broke last time" → `caveat`
- "We learned that X" → `learning`

### Entity key conventions

- Person: full name as `entity_name`, email as `entity_key`
- Company: brand name as `entity_name`, domain as `entity_key`
- Project: project name as `entity_name`, repo URL as `entity_key`
- File: relative or absolute path as both `entity_name` and `entity_key`

### Naming conventions

Use canonical names. "Michie" not "Michie Y" or "山口". "Synapse Arrows"
not "SA". Consistency makes recall reliable.

## Session ritual using Linksee Memory

At session start, after reading STATE.md and GOALS.md:

```typescript
// Recall about the active project
recall("KanseiLink")

// Recall about the user (if it's not your usual user)
recall("Michie")

// Recall about a specific file you're about to touch
recall_file("/path/to/load-bearing-file.ts")
```

At session end (or after major insights):

```typescript
// Save what you learned
remember({...})
```

## When to use Linksee Memory vs the 4-file structure

Both are persistent state. They serve different purposes:

| Question | Look in |
|---|---|
| "What is this project trying to do this quarter?" | GOALS.md |
| "What's the production state right now?" | STATE.md |
| "Why did we choose option B over A in commit Y?" | DECISIONS.md |
| "What's the danger I should know about touching file Z?" | Linksee Memory `recall_file` |
| "What did we learn from incident X?" | Linksee Memory `recall("X")` + `07-learnings/` |
| "What does Michie value / how does she think?" | Linksee Memory `recall("Michie")` |
| "What's the precedent for this kind of decision?" | Linksee Memory `recall(concept)` |

Rule of thumb: **Project-scoped, structural** → 4-file. **Cross-project,
narrative, semantic** → Linksee Memory.

## Anti-patterns

### Storing implementation in caveat layer
Caveats are pain lessons, forget-protected. Don't fill them with neutral
"how to" content. That bloats the protected pool.

### Importance inflation
If everything is 0.9+, nothing is. Reserve high importance for genuine
foundational entries.

### Storing PII or secrets
Linksee Memory is local-only but still a database. Don't put API keys,
passwords, or sensitive customer data in `content`.

### Forgetting to use it
Linksee Memory only helps if agents actually recall on session start. The
CLAUDE.md preamble enforces this.

## Tooling

- MCP server: `@linksee/memory` (npm)
- Install: `npx linksee-memory init`
- Config: `~/.linksee-memory/memory.db` (SQLite, local)
- Tools: `remember`, `recall`, `recall_file`, `update_memory`, `forget`,
  `list_entities`, `consolidate`, `read_smart`

## Public availability

Open source, MIT. Listed on Glama and the official MCP Registry. Other
solo founders are encouraged to adopt the same patterns — every additional
adopter strengthens the operating-system thesis (see
`00-principles/self-similar-architecture.md`).

## See also

- `00-principles/self-similar-architecture.md` — why this is the OS-layer-3
  component
- `02-process/4-file-structure.md` — the partner pattern (project-scoped state)
- `02-process/session-handoff.md` — how Linksee Memory bridges sessions
- `04-tooling-gaps/multi-agent-orchestration.md` — Linksee Memory's role in
  the future Synapse Threads MCP design
