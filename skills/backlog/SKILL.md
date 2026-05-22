---
name: backlog
description: Use when creating or populating a product backlog. Generates user stories from existing product docs, prioritizes them, and writes to 05_scrum/.
---

# Backlog

Generate a prioritized product backlog. Writes to `05_scrum/backlog.md`.

## Process

```
Scan context → Identify epics → Per epic: stories → Acceptance criteria → Priority → Write
```

## Step 0 — Scan context (critical)

Read the following if they exist:
- `01_product/01_prd.md` → product scope and value
- `01_product/05_product_journey.md` → user journey stages
- `02_business/domain_model.md` → entities and operations
- `03_design/ux_spec.md` → screens and flows

Tell the user: "I found [list of docs]. I'll derive the backlog from these. Tell me if anything is outdated."

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What is the scope of this backlog? (all features / specific sprint / MVP only)" (AskUserQuestion options: Full product / MVP only / Next sprint / Specific feature)

**Q2 (if MVP):** "What is the absolute minimum the product must do to deliver value to the first user?" (free text)

**Q3:** "What functionality is OUT of scope for this backlog?" (free text — prevents story creep)

**Q4:** "How should stories be prioritized?" (options: MoSCoW / Business value + effort / User journey order / WSJF)

## Epic Generation

From the scanned docs, propose epics. Tell the user:
"Based on the docs, I propose these epics: [list]. Correct, add, or remove any."

Confirm the epic list before generating stories.

## Story Generation

For each epic, generate 3-7 stories using this format:

```
As a [persona], I want to [action], so that [outcome].

Acceptance criteria:
- [ ] [criterion 1]
- [ ] [criterion 2]
- [ ] [criterion 3]

Story points: [1/2/3/5/8]
Priority: [Must/Should/Could/Won't]
```

After generating, ask the user: "Are there missing stories? Any that should be split or merged?" (free text)

## Document Generation

```markdown
# Product Backlog

**Project:** [name]
**Scope:** [Q1]
**Date:** [today]
**Prioritization:** [Q4]

## Out of Scope

[Q3]

---

## Epic 1: [Epic Name]

**Goal:** [what this epic achieves for the user]

### Story 1.1

**As a** [persona], **I want to** [action], **so that** [outcome].

**Acceptance criteria:**
- [ ] [criterion]
- [ ] [criterion]

**Story points:** [estimate]
**Priority:** [Must/Should/Could/Won't]

---

[Repeat per story and epic]

## Backlog Summary

| Epic | Stories | Total SP | Priority |
|------|---------|----------|----------|
| [Epic 1] | [n] | [total] | Must |
```

## File Output

Write to `05_scrum/backlog.md`. Create folder if missing.
