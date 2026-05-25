---
name: product-journey
description: "Use when creating a Product Journey document. Maps the user's full experience from first contact through recurring use using industry-standard journey mapping structure: Actor → Stage → Goal → Actions → Touchpoints → Emotions → Pain points → Opportunities. Outputs Slice signals per stage that slice-discovery can consume. Writes to docs/01_product/."
---

# Product Journey

Interview the user to map the full product experience using industry-standard journey mapping structure. Write to `docs/01_product/05_product_journey.md`.

## Structure

```
Actor → Stage → Goal → Actions → Touchpoints → Emotions → Pain points → Opportunities → Slice signals
```

---

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root
- **Multiple results:** ask user which one to use
- **No result:** use `docs/` and create it if missing

---

## Step 0 — Scan context

Read the following if they exist:

- `docs/01_product/01_prd.md` → primary user, core problem, out-of-scope items, and **Section 8: Slice signals** (signals already captured during the PRD interview)
- `docs/01_product/04_personas.md` → persona name, context, goals

Extract: who the primary user is, what their core problem is, what success looks like. Use this to ground the interview — do not re-ask what's already documented.

Also extract PRD Slice signals (if section 8 exists) and carry them forward — they will be merged into the relevant Journey stage's Slice signals during document generation, avoiding duplication.

---

## Interview

One question at a time using AskUserQuestion.

**Q1:** "What are the main stages of the user's journey — from first contact to regular use? Name them in order."

Example stages: Discovery → Onboarding → First value → Regular use → Retention risk  
Let the user define their own. Do not impose a template.

---

For **each stage** the user defines, ask the following in sequence:

**Q2 — Goal:** "At [stage name]: what does the user want to achieve? How does this stage goal connect to the product's overall purpose?"

**Q3 — Actions & triggers:** "At [stage name]: what specific actions does the user take? What triggers each action — what makes the user decide to act?"

**Q4 — Touchpoints:** "At [stage name]: what does the user interact with? (screens, buttons, emails, notifications, people, physical objects)"

**Q5 — Emotional state:** "At [stage name]: what is the user's emotional state? Use a scale if helpful: frustrated → neutral → confident → delighted."

**Q6 — Pain points:** "At [stage name]: what can go wrong? What would cause the user to stop or fail at this stage?"

**Q7 — Opportunities:** "At [stage name]: what one change would most improve this stage for the user?"

---

After all stages:

**Q8 — Critical moment:** "At what exact point does the user decide to keep using the product — or abandon it?"

**Q9 — End state:** "At the end of a successful journey, how is the user different from when they started? What changed for them?"

**Q10 — External friction:** "Are there any stages where the user cannot proceed without something outside their control — waiting for approval, connectivity, a third party, a physical process?"

---

## Document Generation

```markdown
# Product Journey

**Project:** [name from PRD]
**Date:** [today]
**Primary actor:** [from personas or PRD]

## Journey Overview

[2–3 sentence arc: from first contact to regular use, what transforms for the user]

**Critical moment:** [Q8 — the decision point]

---

## Stage [N]: [Stage Name]

**Goal:** [Q2 — what the user wants to achieve at this stage, and how it connects to the product's purpose]

**Actions and triggers:**
- User: [action] — triggered by [what]
- User: [action] — triggered by [what]

**Touchpoints:**
- [screen / email / notification / person / object]

**Emotional state:** [Q5 — emotion label or scale position]

**Pain points:**
- [Q6 — what can go wrong]

**Opportunities:**
- [Q7 — what would most improve this stage]

**Stage ID:** S-[N] *(e.g. S-1, S-2 — sequential, used by slices-discovery to reference this stage)*

**Entities:** [comma-separated list of domain entities involved at this stage — e.g. User, Session, Transaction]

**Slice signals:**
- [plain-language description of what the system must support — no tech prescriptions]
- [merge any PRD Slice signals that belong to this stage here]
- Example: "User needs to identify themselves before seeing personalized content"
- Example: "System must remember user's progress between sessions"

---

[Repeat Stage block for each stage]

---

## End State

[Q9 — how the user is different at the end of a successful journey]

---

## External Friction & Risks

| Stage | Friction | Risk / Assumption |
|-------|----------|-------------------|
| [stage name] | [what the user cannot control] | [assumption the team must validate] |

*This section is for the tech team. It does not change the journey narrative above.*
```

---

## Slice signals guidance

Each stage's structured block must include:
- **Stage ID** — sequential (`S-1`, `S-2`, …). `slices-discovery` uses this as a stable reference key.
- **Entities** — comma-separated domain entity names. `slices-discovery` uses these to propose scope and data questions.
- **Slice signals** — plain-language descriptions of what the system must support. Merge PRD signals that belong to this stage here.

Slice signals must be:
- Written in plain language — what the user needs, not how to build it
- Free of architectural decisions (no "OAuth", "REST API", "database", "PostgreSQL")
- Actionable: `slices-discovery` uses them to pre-populate Q4 (scope) and Q7 (data entities)

Good: "User needs to identify themselves before proceeding"  
Bad: "Implement JWT auth with refresh tokens"

Good: "System must show the user their past activity"  
Bad: "Build a history table in PostgreSQL"

---

## File Output

Write to `docs/01_product/05_product_journey.md`. Create folder if missing.
