---
name: product-journey
description: Use when creating a Product Journey document. Maps the user's experience from first contact through recurring use and long-term retention. Writes to 01_product/.
---

# Product Journey

Interview the user to map the full product experience. Write to `docs/01_product/05_product_journey.md`.

## Process

```
Scan context → Journey stages → Per stage: user state, actions, system response, emotion → Write
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

Read `docs/` personas and PRD if they exist. Extract: who the user is, what their goal is.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What are the main stages of the user's journey? (from first contact to regular use)"
Example stages: Discovery → Onboarding → First value → Regular use → Churn risk
(free text — let user define their own stages)

For each stage the user defines, ask:

**Q2a:** "At [stage name]: What does the user want to achieve?" (free text)

**Q2b:** "At [stage name]: What actions does the user take? What does the system do in response?" (free text)

**Q2c:** "At [stage name]: What is the user's emotional state? What could go wrong here?" (free text)

**Q3:** "What is the most critical moment — when does the user decide to keep using or abandon the product?" (free text)

**Q4:** "What does success look like at the END of the journey? How is the user different than at the start?" (free text)

## Document Generation

```markdown
# Product Journey

**Project:** [name]
**Date:** [today]

## Journey Overview

[Brief description of the arc: from first contact to regular use]

**Critical moment:** [Q3]

---

## Stage 1: [Stage Name]

**User goal:** [Q2a]

**Actions and system response:**
- User: [action]
- System: [response]
- [...]

**Emotional state:** [Q2c — emotion]

**Risk at this stage:** [Q2c — what could go wrong]

---

[Repeat for each stage]

## End State

[Q4 — how the user is different at the end of a successful journey]
```

## File Output

Write to `docs/01_product/05_product_journey.md`. Create folder if missing.
