---
name: product-goal
description: Use when creating a Product Goal document. Defines the measurable outcome the product aims to achieve in a specific time horizon. Writes to 01_product/.
---

# Product Goal

Interview the user to define the product's measurable goal. Write to `01_product/02_product_goal.md`.

## Process

```
Scan context → Time horizon → Goal statement → Key metrics → Validation criteria → Write
```

## Step 0 — Scan context

Read `01_product/01_prd.md` if exists. Extract product name and success indicators. Tell user what you found.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What time horizon is this goal for?" (options: 3 months / 6 months / 1 year / Other)

**Q2:** "Complete this: 'By [time horizon], the product achieves [measurable outcome] for [user type].'" (free text)

**Q3:** "How will you measure if this goal is achieved? List 2-4 specific metrics with numbers." (free text)
Example: "70% of users open the app at least 3x per week after 30 days", "NPS > 40 at 3 months"

**Q4:** "What is the minimum acceptable outcome? (what would still count as success even if the full goal isn't met)" (free text)

**Q5:** "What would make this goal fail? (top 2-3 risks)" (free text)

## Document Generation

```markdown
# Product Goal

**Project:** [name]
**Time horizon:** [Q1]
**Date:** [today]

## Goal Statement

By [Q1], [Q2 — full goal statement].

## Success Metrics

| Metric | Target | Measurement method |
|--------|--------|-------------------|
| [metric 1] | [target] | [how measured] |
| [metric 2] | [target] | [how measured] |

## Minimum Acceptable Outcome

[Q4]

## Risk to Goal

1. [Q5 risk 1]
2. [Q5 risk 2]
```

## File Output

Write to `01_product/02_product_goal.md`. Create folder if missing.
