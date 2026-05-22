---
name: definition-of-done
description: Use when creating a Definition of Done for a Scrum team. Defines the criteria a user story must meet before it is considered complete. Writes to 05_scrum/.
---

# Definition of Done

Interview the user to define when a story is truly complete. Write to `05_scrum/definition_of_done.md`.

## Process

```
Scan context → Code criteria → Testing criteria → Documentation criteria → Deployment criteria → Write
```

## Step 0 — Scan context

Read `01_product/01_prd.md` and any tech architecture docs if they exist.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What CODE standards must be met?" (free text)
Example: "Code reviewed by at least 1 other dev", "No linting errors", "Follows agreed naming conventions"

**Q2:** "What TESTING requirements must be met?" (free text)
Example: "Unit tests written and passing", "Happy path manually tested", "Edge cases in acceptance criteria tested"

**Q3:** "What DOCUMENTATION is required?" (free text or N/A)
Example: "API endpoints documented", "README updated if new setup steps", "Decision recorded in decision log"

**Q4:** "What DEPLOYMENT criteria must be met?" (free text)
Example: "Feature deployed to staging", "Feature flag configured", "No regressions in smoke test"

**Q5:** "What PRODUCT criteria must be met?" (free text)
Example: "All acceptance criteria checked", "PO or stakeholder has verified the feature", "Design matches spec"

**Q6:** "Are there non-functional requirements that always apply?" (free text)
Example: "Accessible (WCAG AA)", "Works on mobile", "Response time < 2s"

## Document Generation

```markdown
# Definition of Done

**Project:** [name]
**Date:** [today]

## Purpose

A story is Done only when ALL of the following are true. Partial completion is not Done.

## Criteria

### Code
- [ ] [Q1 criterion 1]
- [ ] [Q1 criterion 2]

### Testing
- [ ] [Q2 criterion 1]
- [ ] [Q2 criterion 2]

### Documentation
- [ ] [Q3 criterion 1]

### Deployment
- [ ] [Q4 criterion 1]
- [ ] [Q4 criterion 2]

### Product
- [ ] [Q5 criterion 1]
- [ ] [Q5 criterion 2]

### Non-Functional (always applies)
- [ ] [Q6 criterion 1]

## When to Waive a Criterion

A criterion can only be waived when:
1. The reason is documented in the story
2. A follow-up story is created immediately to address it
3. The team explicitly agrees (not just one person)

## Ceremony

DoD is reviewed at sprint review. Any story that doesn't meet all criteria is moved back to the backlog.
```

## File Output

Write to `05_scrum/definition_of_done.md`. Create folder if missing.
