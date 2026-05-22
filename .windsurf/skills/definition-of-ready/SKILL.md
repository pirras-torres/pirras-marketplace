---
name: definition-of-ready
description: Use when creating a Definition of Ready for a Scrum team. Defines the criteria a user story must meet before it can enter a sprint. Writes to 05_scrum/.
---

# Definition of Ready

Interview the user to define when a story is ready for sprint planning. Write to `05_scrum/definition_of_ready.md`.

## Process

```
Scan context → Team context → Criteria per category → Exceptions → Write
```

## Step 0 — Scan context

Read `05_scrum/backlog.md` if exists. Use story format as reference for criteria.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What must be true about a story's DESCRIPTION before it enters a sprint?" (free text)
Example: "Written in user story format", "Problem is clearly defined", "No ambiguous terms"

**Q2:** "What must be true about ACCEPTANCE CRITERIA?" (free text)
Example: "At least 3 criteria", "Each criterion is testable", "Happy path + at least 1 failure case"

**Q3:** "What DESIGN artifacts must exist?" (free text or N/A)
Example: "UX wireframe approved", "Copy reviewed", "Edge cases documented"

**Q4:** "What TECHNICAL preconditions must exist?" (free text or N/A)
Example: "Architecture decision made", "API contract defined", "Dependencies identified"

**Q5:** "What is the maximum story size allowed? (if larger, must be split)" (options: 1 day / 3 days / 1 sprint / No limit)

**Q6:** "What is the process to mark a story as Ready? (who approves, when)" (free text)

## Document Generation

```markdown
# Definition of Ready

**Project:** [name]
**Date:** [today]

## Purpose

A story is Ready when the team has enough information to start it, complete it in a sprint, and test it.

## Criteria

### Description
- [ ] [Q1 criterion 1]
- [ ] [Q1 criterion 2]

### Acceptance Criteria
- [ ] [Q2 criterion 1]
- [ ] [Q2 criterion 2]

### Design (if applicable)
- [ ] [Q3 criterion 1]

### Technical
- [ ] [Q4 criterion 1]

### Size
- [ ] Story fits in [Q5]
- [ ] If larger, it has been split

## Process

[Q6 — who marks ready, when, how]

## Exceptions

[Any story types that bypass standard DoR, and why]
```

## File Output

Write to `05_scrum/definition_of_ready.md`. Create folder if missing.
