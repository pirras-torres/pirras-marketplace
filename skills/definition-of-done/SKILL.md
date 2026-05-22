---
name: definition-of-done
description: Use when creating a Definition of Done for a Scrum team. Reads Product Goal, principles, architecture, and slice risk docs to suggest criteria, then interviews the user to confirm. Writes to 05_scrum/.
---

# Definition of Done

Define when a story and a sprint increment are truly complete. Reads existing docs to suggest criteria — user confirms or adjusts.

DoD applies to every increment. A story is Done only when ALL criteria are met. Partial is not Done.

## Process

```
Scan docs → Derive suggested criteria → User confirms per category → Write
```

## Step 0 — Deep scan

Read ALL of the following that exist:

| Doc | What to extract |
|-----|----------------|
| `01_product/02_product_goal.md` | Outcome criteria — what does "valuable increment" mean for this product? |
| `01_product/03_product_principles.md` | Quality standards embedded in principles (e.g., "clarity over completeness" → UI must show clear state) |
| `03_design/ux_spec.md` | UI states to verify: empty states, error states, interaction rules |
| `03_design/ui_spec.md` | Visual correctness to verify: component usage, spacing, states |
| `04_tech/backend_architecture.md` | Testing strategy, deployment pipeline, API standards |
| `04_tech/frontend_architecture.md` | Testing framework, error handling patterns, accessibility |
| `06_decisions/risk_docs.md` | Risk mitigations that must be verified before Done |

After reading, derive suggested criteria per category. Tell user:
> "Based on your docs, I'm suggesting these DoD criteria. Review each and adjust."

---

## Interview — confirm per category

**Q1 — Code quality:**
Suggest based on architecture docs: e.g., "Code reviewed. No linting errors. Follows naming conventions from [architecture doc]."
**"Adjust code quality criteria?"** (free text or "Looks good")

**Q2 — Testing:**
Suggest based on testing strategy found: e.g., "Unit tests for business logic. Happy path and key failure cases covered. All tests pass."
If no testing strategy found: ask "What testing is required before Done?" (free text)
**"Adjust testing criteria?"** (free text or "Looks good")

**Q3 — Behavior visible to user:**
Suggest based on ux_spec: e.g., "All acceptance criteria verified. Empty state shows correctly. Error state shows correct message. No broken UI states."
**"Adjust behavior verification criteria?"** (free text or "Looks good")

**Q4 — Deployment:**
Suggest based on architecture: e.g., "Deployed to [staging/test environment]. No regressions in smoke test. Feature available for review."
**"Adjust deployment criteria?"** (free text or "Looks good" or "Not applicable yet")

**Q5 — Documentation:**
Suggest: "If a business rule, architecture decision, or UX flow changed: canonical doc updated. If a new decision was made: logged in decision_docs."
**"Adjust documentation criteria?"** (free text or "Looks good")

**Q6 — Non-functional:**
Derive from PRD/principles/ux_spec: e.g., "Accessible on [platform]. Works at [stated performance target]. No console errors."
**"Any additional non-functional requirements?"** (free text or "None")

**Q7 — Product verification:**
**"Who verifies the increment and when? (e.g., 'PO verifies before sprint review')"** (free text)

---

## Document Generation

```markdown
# Definition of Done

**Project:** [name]
**Date:** [today]

## Purpose

An increment is Done when ALL criteria below are true. This applies to every story and to the sprint as a whole.
Partial completion is not Done. Stories that don't meet DoD return to backlog.

## Criteria

### Code Quality
- [ ] [Q1 criteria]

### Testing
- [ ] [Q2 criteria]

### Behavior (user-visible)
- [ ] [Q3 criteria]

### Deployment
- [ ] [Q4 criteria — or "Not applicable: [reason]"]

### Documentation
- [ ] If business rule, architecture, or UX changed → canonical doc updated
- [ ] If new decision made → logged in `06_decisions/`
- [ ] [Q5 additional criteria]

### Non-Functional
- [ ] [Q6 criteria — or "None defined"]

## Verification

[Q7 — who verifies, when, in what context]

## Waiving a Criterion

A criterion may be waived when:
1. Reason is documented in the story
2. Follow-up story created immediately
3. Explicit team agreement recorded in sprint plan

## Connection to Docs

[List of docs read — what informs each criterion]
```

## File Output

Write to `05_scrum/definition_of_done.md`. Create folder if missing.

## Quality Check Before Writing

- Every criterion is verifiable — not "good quality" but "tests pass", "PO verified", "deployed to staging"
- Behavior criteria reference specific states from ux_spec if it exists
- Documentation criterion is explicit: canonical docs update when reality changes
- Non-functional criteria derived from actual project constraints, not generic
