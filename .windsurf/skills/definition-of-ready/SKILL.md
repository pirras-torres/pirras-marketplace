---
name: definition-of-ready
description: Use when creating a Definition of Ready for a Scrum team. Reads existing architecture and product docs to suggest criteria, then interviews the user to confirm. Writes to 05_scrum/.
---

# Definition of Ready

Define when a PBI can enter a sprint. Reads existing docs to suggest criteria — user confirms or adjusts.

A story is Ready when the team has enough to start it, complete it in a sprint, and verify it. Criteria must be checkable, not aspirational.

## Process

```
Scan docs → Derive suggested criteria per category → User confirms/adjusts → Write
```

## Step 0 — Deep scan

Read ALL of the following that exist:

| Doc | What to extract |
|-----|----------------|
| `01_product/01_prd.md` | Product scope — any features that need special DoR? |
| `01_product/03_product_principles.md` | Quality standards that apply before sprint entry |
| `02_business/domain_model.md` | Complex entities that need UX/data design before coding |
| `02_business/business_rules.md` | Rules that require architecture decision before implementing |
| `03_design/ux_spec.md` | Which flows/screens need UX documented before sprint |
| `04_tech/backend_architecture.md` | API contract requirements, auth decisions needed per story |
| `04_tech/frontend_architecture.md` | Testing framework, component patterns needed before sprint |

After reading, derive suggested criteria per category. Tell user:
> "Based on your docs, I'm suggesting these DoR criteria. Review each category and adjust."

---

## Interview — confirm per category

For each category, present suggested criteria and ask for confirmation or changes. One category at a time.

**Q1 — Story description:**
Present suggestion: e.g., "Written in user story format. Problem clearly defined. No ambiguous domain terms (references domain model)."
**"Does this match your DoR for story description, or do you want to change it?"** (free text or "Looks good")

**Q2 — Acceptance criteria:**
Present suggestion: e.g., "At least 3 criteria. Each criterion is testable (Given/When/Then or equivalent). Happy path + at least 1 failure case."
**"Adjust acceptance criteria requirements?"** (free text or "Looks good")

**Q3 — Design/UX:**
If ux_spec.md exists: suggest "UX flow for affected screen documented in ux_spec.md. Empty and error states defined."
If not: suggest "UX described in story with screen states."
**"Adjust design requirements?"** (free text or "Looks good" or "Not required")

**Q4 — Technical preconditions:**
If backend_architecture.md exists: suggest "API endpoint contract defined (request/response schema). Auth method clear."
If business_rules.md has complex rules: suggest "Business rules for this story's domain confirmed in business_rules.md."
If frontend_architecture.md exists: suggest "Component pattern for new UI elements decided."
**"Adjust technical requirements?"** (free text or "Looks good" or "Not required")

**Q5 — Size:**
**"Maximum story size before it must be split?"** (AskUserQuestion options: 1 day / 3 days / 1 sprint / No limit)

**Q6 — Process:**
**"Who confirms a story is Ready and when? (e.g., 'dev team + PO during refinement, 2 days before sprint')"** (free text)

---

## Document Generation

```markdown
# Definition of Ready

**Project:** [name]
**Date:** [today]

## Purpose

A PBI is Ready when the team has enough information to start it, finish it in one sprint, and verify it. No story enters a sprint without meeting all criteria below.

## Criteria

### Story Description
- [ ] [Q1 criteria]

### Acceptance Criteria
- [ ] [Q2 criteria]

### Design / UX
- [ ] [Q3 criteria — or "Not required for this project"]

### Technical Preconditions
- [ ] [Q4 criteria]

### Size
- [ ] Story fits within [Q5]
- [ ] If larger: split before entering sprint

## Ready Process

[Q6 — who confirms, when]

## Exceptions

Stories that bypass standard DoR must document why and have team agreement recorded in the sprint plan.

## Connection to Docs

These criteria reference:
[List of docs that were read — links to what informs each criterion]
```

## File Output

Write to `05_scrum/definition_of_ready.md`. Create folder if missing.

## Quality Check Before Writing

- Every criterion is checkable — binary yes/no answer possible
- No criterion requires judgment calls without a reference doc
- Size criterion is explicit
- Process names who is responsible, not just "team"
