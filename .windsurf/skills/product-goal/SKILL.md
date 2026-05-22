---
name: product-goal
description: Use when creating a Product Goal document. Reads existing PRD success indicators as a starting point, then refines with time horizon and specific metrics. Writes to 01_product/.
---

# Product Goal

Define the measurable outcome the product aims to achieve. Starts from PRD success indicators — refines them into a time-bound goal with specific metrics.

## Process

```
Read PRD → Present existing success indicators → Time horizon → Refine goal statement
→ Metrics → Minimum acceptable outcome → Risks → Write
```

## Step 0 — Read PRD

Read `01_product/01_prd.md`. Extract:
- Product name
- Product promise
- Success indicators (section 7)
- Target user

Tell user:
> "I found the PRD for [product name]. Success indicators already defined: [list]. I'll use these as the basis for the Product Goal."

If no PRD exists: ask for brief product description and intended success (2-3 sentences) before continuing.

---

## Step 1 — Time horizon

**Q1:** "What time horizon is this Product Goal for?" (AskUserQuestion options: 3 months / 6 months / 1 year / Other)

---

## Step 2 — Goal statement

**Q2:** "Complete: 'By [time horizon], [product name] achieves [measurable outcome] for [user].'" (free text)

The goal statement must name:
- A specific user type (from personas or PRD)
- A measurable outcome (not "users love it")
- A time horizon

If the PRD success indicators suggest a goal, propose one: "Based on the PRD, a possible goal is: [derived statement]. Use this or write your own."

---

## Step 3 — Success metrics

Present existing PRD success indicators and ask to refine:

**Q3:** "The PRD defines these success indicators: [list]. Convert them into specific metrics with numbers and measurement methods." (free text)
Example: "70% of users open the app 3+ times/week after 30 days, measured via app events"

Require at least 2 metrics. Each metric needs:
- What is measured
- Target value
- How it's measured

---

## Step 4 — Minimum acceptable outcome

**Q4:** "What is the minimum acceptable outcome? What would still count as success even if the full goal isn't met?" (free text)

This is the floor, not the ceiling.

---

## Step 5 — Goal risks

**Q5:** "What are the top 2-3 risks that could prevent reaching this goal?" (free text)

---

## Document Generation

```markdown
# Product Goal

**Project:** [name]
**Time horizon:** [Q1]
**Date:** [today]

## Goal Statement

By [Q1], [Q2 — full goal statement].

## Success Metrics

| Metric | Target | How measured |
|--------|--------|--------------|
| [metric 1] | [target] | [method] |
| [metric 2] | [target] | [method] |

## Minimum Acceptable Outcome

[Q4 — the floor for success]

## Risks to Goal

1. [Q5 risk 1]
2. [Q5 risk 2]
[3. Q5 risk 3 if provided]

## Source

Derived from PRD success indicators: `01_product/01_prd.md#7-success-indicators`
```

## File Output

Write to `01_product/02_product_goal.md`. Create folder if missing.

## Quality Check Before Writing

- Goal statement names user, outcome, and time horizon
- Every metric has a target number and measurement method
- Minimum acceptable outcome is lower than the full goal (not the same)
- Risks are specific to this product and goal (not generic)
