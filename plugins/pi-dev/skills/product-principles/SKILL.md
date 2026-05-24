---
name: product-principles
description: Use when creating Product Principles for a software project. Defines the decision-making rules that guide product choices. Writes to 01_product/.
---

# Product Principles

Interview the user to define the product's guiding principles. Write to `docs/01_product/03_product_principles.md`.

## What Are Product Principles

Principles are decision-making rules. When the team faces a trade-off, principles resolve it.
A good principle: takes a position, explains why, and can be violated intentionally when noted.

Bad: "We value quality." (not a decision rule)  
Good: "Clarity over completeness — show less if it means the user understands more." (resolves trade-offs)

## Process

```
Scan context → 3 trade-off scenarios → 4 anchoring questions → Derive principles → Write
```

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Scan context

Read `docs/01_product/01_prd.md` if exists. Extract product vision and value proposition. Use it to make questions specific to this product, not generic.

## Interview (one question at a time with AskUserQuestion)

**Trade-off scenarios** — ask each separately:

**Q1a:** "Describe a real decision you made about this product where you had to choose between two valid options. What were the options and what did you choose?" (free text)

**Q1b:** "Describe a second decision with a trade-off — different from the first." (free text)

**Q1c:** "Describe a third trade-off decision." (free text)

Each answer becomes raw material for one principle. If the user struggles, offer an example: "For example: 'We chose to show less data on the main screen rather than showing everything — prioritized clarity over completeness.'"

**Anchoring questions:**

**Q2:** "When this product must choose between simplicity and power/flexibility, which does it favor?" (free text)

**Q3:** "When this product must choose between speed of delivery and quality/polish, which does it favor?" (free text)

**Q4:** "What is the ONE thing this product must never do, even if it would make it more popular or easier to build?" (free text)

**Q5:** "What is the ONE thing this product always does, even when it adds complexity or cost?" (free text)

## Document Generation

From Q1a–Q1c and Q2–Q5, derive 4–7 principles. Each principle must:
- Have a name (3–6 words, active voice, takes a position)
- Have a rationale (1–2 sentences why this product specifically holds this principle)
- Have a concrete example of what it means in practice for this product

Order principles by importance — the first one wins when two conflict.

```markdown
# Product Principles

**Project:** [name]
**Date:** [today]

## How to Use These Principles

When facing a trade-off, check which principle applies. If two principles conflict, use the order below — earlier principles take precedence.

## Principles

### 1. [Principle Name — active voice, takes a position]

[Rationale: why this product holds this principle — 1-2 sentences]

**In practice:** [Concrete example specific to this product]

---

[Repeat for each principle — 4–7 total]
```

## File Output

Write to `docs/01_product/03_product_principles.md`. Create folder if missing.

## Quality Check Before Writing

- Every principle takes a position (not "we value X" but "X over Y when Z")
- Every principle has a concrete example from this product's domain
- At least one principle came from a real trade-off the user described
- No two principles say the same thing in different words
