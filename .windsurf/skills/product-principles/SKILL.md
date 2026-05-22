---
name: product-principles
description: Use when creating Product Principles for a software project. Defines the decision-making rules that guide product choices. Writes to 01_product/.
---

# Product Principles

Interview the user to define the product's guiding principles. Write to `01_product/03_product_principles.md`.

## What Are Product Principles

Principles are decision-making rules. When the team faces a trade-off, principles resolve it.
A good principle: takes a position, explains why, and can be violated intentionally when noted.

Bad: "We value quality." (not a decision rule)
Good: "Clarity over completeness — show less if it means the user understands more." (resolves trade-offs)

## Process

```
Scan context → Collect trade-off scenarios → Extract principles → Prioritize → Write
```

## Step 0 — Scan context

Read `01_product/01_prd.md` if exists. Extract product vision and value proposition.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "Think of a decision you or the team made about this product. What was the trade-off and what did you choose?" (free text)
Ask this 3 times (repeat Q1 for 3 different decisions). Each answer is raw material for a principle.

**Q2:** "When you must choose between [simplicity vs power], what does this product favor?" (free text)

**Q3:** "When you must choose between [speed of delivery vs quality], what does this product favor?" (free text)

**Q4:** "What is the ONE thing this product must never do, even if it would make it more popular?" (free text)

**Q5:** "What is the ONE thing this product always does, even when it adds complexity?" (free text)

## Document Generation

From the user's answers, derive 4-7 principles. Each principle:
- Has a name (3-6 words, active voice)
- Has a rationale (1-2 sentences why)
- Has an example of what it means in practice

```markdown
# Product Principles

**Project:** [name]
**Date:** [today]

## How to Use These Principles

When facing a trade-off, check which principle applies. If two principles conflict, use the order below — earlier principles take precedence.

## Principles

### 1. [Principle Name]

[Rationale in 1-2 sentences]

**In practice:** [Concrete example]

---

[Repeat for each principle — 4-7 total]
```

## File Output

Write to `01_product/03_product_principles.md`. Create folder if missing.
