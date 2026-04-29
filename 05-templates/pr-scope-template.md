<!--
{PROJECT_NAME} — PR template enforcing scope-locks Layer 2.
See https://github.com/michielinksee/synapse-arrows-playbook/blob/main/02-process/scope-locks.md

Save this file as: .github/PULL_REQUEST_TEMPLATE.md
-->

## Scope of this PR

Check exactly the boxes that apply. Anything unchecked is a "DO NOT TOUCH"
zone. CI will fail if your diff includes files outside the checked scopes.

- [ ] Chat / response logic
- [ ] UI components
- [ ] Database schema
- [ ] LLM prompts / model selection
- [ ] Build / deployment / infra
- [ ] Tests only
- [ ] Documentation only
- [ ] Other: ___

## Files I expect to change

List every file you intend to modify. CI compares this list against the
actual diff and fails on mismatches.

```
- src/features/...
- src/...
- __tests__/...
```

## Linked spec docs

Which `docs/specs/*.md` does this PR touch or reference?

- `docs/specs/...`

If this PR changes feature behavior but does NOT update a spec doc,
provide explicit justification:

`[no-spec-change: <reason>]`

## Locked path acknowledgment

If this PR modifies any file listed in `.locked-paths`, declare here:

- [ ] No locked paths affected
- [ ] Locked paths affected — `[unlock: <reason>]` in commit message AND
      DECISIONS.md entry attached

## Test plan

- [ ] Existing tests pass locally
- [ ] New tests added for the change (or N/A — describe why)
- [ ] Visual regression baseline updated (if UI changed)
- [ ] Manual smoke check on staging

## Reversibility

- [ ] Easily reversible (revert PR works)
- [ ] Partially reversible (data migration / DB schema involved)
- [ ] Hard to reverse (describe rollback plan)

## DECISIONS.md / Linksee Memory

- DECISIONS.md entry: `YYYY-MM-DD-<id>` (or N/A)
- Linksee Memory pin: yes / no — entity name: `{PROJECT_NAME}`

---

🤖 This template enforces Synapse Arrows Playbook scope-locks discipline.
