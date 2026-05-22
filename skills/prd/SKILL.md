---
name: prd
description: Use when creating a Product Requirements Document (PRD) for a new or existing software project. Interviews the user section by section and writes the document to disk.
---

# Product Requirements Document (PRD)

Interview the user section by section using AskUserQuestion. Write the resulting document to `01_product/01_prd.md`.

## Process

```
Scan context → Section 1: Problem → Section 2: Vision → Section 3: Identity
→ Section 4: Target User → Section 5: Value Proposition → Section 6: Scope
→ Section 7: Success Indicators → Generate doc → Write to disk
```

## Step 0 — Scan context

Before asking anything:
- Check if `01_product/01_prd.md` already exists. If yes, ask the user if they want to update or create new.
- Look for any other context files in the project (README, CLAUDE.md, existing docs) to pre-fill answers you can infer. Tell the user what you found.

## Step 1 — Project basics

Ask with AskUserQuestion (one question at a time):

**Q1:** "What is the name of the project?" (free text — use Other option)

**Q2:** "In one sentence: what problem does this product solve for the user?" (free text)

**Q3:** "Who is the primary user? Describe them in one sentence." (free text)

After each answer, confirm understanding before moving on. If the answer is vague, ask one clarifying follow-up.

## Step 2 — Problem deep dive

Ask the user to describe the problem in more detail. Use AskUserQuestion:

**Q4:** "What are the top 3 pain points the user has today without this product?" (free text — expect comma-separated or bullet points)

**Q5:** "What does the user currently use instead? (apps, spreadsheets, manual process, nothing)" (free text)

## Step 3 — Vision and identity

**Q6:** "What is the product vision? Complete this: 'This product helps [user] to [outcome] so they can [higher goal].'" (free text)

**Q7:** "What is the product's promise in one sentence? Example: 'Your finances clear, even across multiple accounts.'" (free text)

**Q8:** "What is the product name? (internal codename and/or commercial name)" (free text)

## Step 4 — Target user boundaries

**Q9:** "Who is NOT the target user? List types of users this product does NOT serve." (free text)

This section is critical. A sharp non-user definition prevents scope creep.

## Step 5 — Value proposition

**Q10:** "What are the top 3 things the user can do or know because of this product that they couldn't before?" (free text)

**Q11 (optional):** "Is there a key differentiator vs existing solutions? What makes this product different?" (free text)

## Step 6 — Scope boundaries

**Q12:** "What is explicitly OUT of scope for this product? (features or use cases this product will never cover)" (free text)

## Step 7 — Success indicators

**Q13:** "How will you know the product is succeeding? List 2-4 measurable indicators." (free text)
Example: "User opens app 3x/week", "User answers 'I understand my finances' after 1 week"

## Document Generation

After all sections, generate the PRD in this structure:

```markdown
# PRD - [Product Name]

**Project:** [internal name]
**Commercial name:** [commercial name or PENDING]
**Status:** Foundational PRD
**Date:** [today's date]

## 1. Problem

[Problem statement from Q2. Expand with pain points from Q4. Mention current alternatives from Q5.]

## 2. Product Vision

[Vision statement from Q6]

**Product promise:** "[Q7]"

## 3. Product Identity

**[Internal name]** is [brief description].
**[Commercial name]** is the proposed commercial name. [PENDING if not confirmed]

## 4. Target User

[Target user from Q3, expanded with context]

The target user typically:
- [Pain point 1]
- [Pain point 2]
- [Pain point 3]

**Not target users:** [Q9 — who is explicitly out of scope]

## 5. Value Proposition

[Product name] delivers [core value] by [how]:
- [Value 1 from Q10]
- [Value 2 from Q10]
- [Value 3 from Q10]

[Differentiator from Q11 if provided]

## 6. Out of Scope

This product does not:
- [Out of scope item 1 from Q12]
- [Out of scope item 2]
- [...]

## 7. Success Indicators

- [Indicator 1 from Q13]
- [Indicator 2]
- [...]
```

## File Output

- Create folder `01_product/` if it doesn't exist
- Write to `01_product/01_prd.md`
- After writing, show the user the file path and ask if they want to review or adjust any section

## Quality Check Before Writing

Before writing the file, verify:
- Problem section answers WHY the product exists, not just what it does
- Target user section has both WHO IS and WHO IS NOT
- Out of scope section has at least 2 explicit items
- Success indicators are measurable (not "users love it")

If any check fails, ask the user for the missing info before writing.
