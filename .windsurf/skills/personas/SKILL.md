---
name: personas
description: Use when creating user personas for a software project. Defines who uses the product, their context, goals, and pain points. Writes to 01_product/.
---

# Personas

Interview the user to define 1-3 product personas. Write to `01_product/04_personas.md`.

## Process

```
Scan context → Number of personas → Per persona: demographics, context, goals, pain points, behaviors → Write
```

## Step 0 — Scan context

Read `01_product/01_prd.md` if exists. Extract target user description and non-user definition.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "How many distinct user types does this product serve?" (options: 1 / 2 / 3)

For each persona (repeat the following block):

**Q2:** "What is a name and short label for this persona? (e.g., 'Laura, the organized saver')" (free text)

**Q3:** "Describe this persona's context. Who are they, what do they do, what tools do they use for this problem today?" (free text)

**Q4:** "What is their primary goal when using this product? What does success look like for them?" (free text)

**Q5:** "What are their top 3 frustrations with their current approach?" (free text)

**Q6:** "What makes this persona different from the other personas? (if more than one)" (free text — skip if only one persona)

**Q7:** "What would make this persona STOP using the product?" (free text)

## Document Generation

```markdown
# Personas

**Project:** [name]
**Date:** [today]

---

## Persona 1: [Name and label]

**Context:** [Q3]

**Primary goal:** [Q4]

**Frustrations today:**
- [frustration 1]
- [frustration 2]
- [frustration 3]

**Churns if:** [Q7]

---

[Repeat for each persona]

## What All Personas Share

[Synthesize common traits and goals across all personas]

## Key Differences Between Personas

[Q6 answers — what distinguishes each]
```

## File Output

Write to `01_product/04_personas.md`. Create folder if missing.
