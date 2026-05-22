---
name: personas
description: Use when creating user personas for a software project. Defines who uses the product, their context, goals, and pain points. Writes to 01_product/.
---

# Personas

Interview the user to define 1-3 product personas. Write to `01_product/04_personas.md`.

## Process

```
Scan context → Number of personas → Persona 1 questions → Persona 2 questions (if needed)
→ Persona 3 questions (if needed) → Synthesis → Write
```

## Step 0 — Scan context

Read `01_product/01_prd.md` if exists. Extract: target user description, non-user definition, pain points already described. Tell user what you found and use it to make questions specific.

## Step 1 — Number of personas

**Q1:** "How many distinct user types does this product serve?" (AskUserQuestion options: 1 / 2 / 3)

---

## Step 2 — Persona 1 (always ask)

**Q2a:** "Persona 1 — What is their name and a short label? (e.g., 'Laura, the organized saver')" (free text)

**Q3a:** "Persona 1 — Describe their context: who are they, what do they do, what tools do they use today for this problem?" (free text)

**Q4a:** "Persona 1 — What is their primary goal when using this product? What does success look like for them?" (free text)

**Q5a:** "Persona 1 — What are their top 3 frustrations with their current approach?" (free text)

**Q6a:** "Persona 1 — What would make them stop using the product?" (free text)

---

## Step 3 — Persona 2 (only if Q1 = 2 or 3)

**Q2b:** "Persona 2 — Name and short label?" (free text)

**Q3b:** "Persona 2 — Context: who are they, what do they do, what tools do they use today?" (free text)

**Q4b:** "Persona 2 — Primary goal and what success looks like?" (free text)

**Q5b:** "Persona 2 — Top 3 frustrations with current approach?" (free text)

**Q6b:** "Persona 2 — What would make them stop using the product?" (free text)

**Q7b:** "What makes Persona 2 different from Persona 1? What do they need that Persona 1 doesn't?" (free text)

---

## Step 4 — Persona 3 (only if Q1 = 3)

**Q2c:** "Persona 3 — Name and short label?" (free text)

**Q3c:** "Persona 3 — Context?" (free text)

**Q4c:** "Persona 3 — Primary goal and success?" (free text)

**Q5c:** "Persona 3 — Top 3 frustrations?" (free text)

**Q6c:** "Persona 3 — Churn trigger?" (free text)

**Q7c:** "What makes Persona 3 different from the others?" (free text)

---

## Document Generation

```markdown
# Personas

**Project:** [name]
**Date:** [today]

---

## Persona 1: [Name and label]

**Context:** [Q3a]

**Primary goal:** [Q4a]

**Frustrations today:**
- [frustration 1]
- [frustration 2]
- [frustration 3]

**Churns if:** [Q6a]

---

[Repeat section for Persona 2 and 3 if applicable]

## What All Personas Share

[Synthesize common traits, goals, and pain points across personas]

## Key Differences Between Personas

[Q7b / Q7c — what distinguishes each]
```

## File Output

Write to `01_product/04_personas.md`. Create folder if missing.

## Quality Check Before Writing

- Each persona has a distinct identity (not just the same user described twice)
- Each has a specific churn trigger (not "they'd stop if product is bad")
- Differences section is explicit — not implied
