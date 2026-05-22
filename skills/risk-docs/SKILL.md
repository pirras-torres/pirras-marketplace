---
name: risk-docs
description: Use when creating a risk register for a software project. Reads existing docs to identify risks, interviews the user, then rates and documents each risk with mitigation. Writes to 06_decisions/.
---

# Risk Register

Identify, rate, and document project risks. Reads existing docs to surface risks automatically — user confirms and adds more.

## Process

```
Scan docs → Derive risk candidates → User confirms + adds → Rate each risk
→ Mitigation per risk → Write
```

## Step 0 — Scan for risk candidates

Read ALL of the following that exist and extract risk candidates:

| Doc | Risk signals |
|-----|-------------|
| `04_tech/backend_architecture.md` | Open decisions → technical risks |
| `04_tech/frontend_architecture.md` | Open decisions → technical risks |
| `02_business/domain_model.md` | Complex invariants → implementation risk |
| `05_scrum/discovery/S*.md` | Pending / blocking items → delivery risks |
| `01_product/01_prd.md` | Out-of-scope assumptions → product risks |
| `01_product/04_personas.md` | Churn triggers → product risks |

Present derived risk candidates:
> "Based on your docs, I identified these potential risks: [list with source]. Confirm which are real risks, and add any I missed."

---

## Step 1 — Confirm and add risks

**Q1:** "From the list above, which risks are real concerns? Remove any that aren't relevant." (free text or "All are valid")

**Q2:** "What additional risks aren't in the list? Think: technical unknowns, user behavior assumptions, external dependencies, team constraints." (free text or "None")

---

## Step 2 — Rate each risk

For each confirmed risk, ask:

**Q3:** "For risk '[risk name]': How likely is it? (High / Medium / Low)" (AskUserQuestion per risk)

**Q4:** "For risk '[risk name]': If it happens, what's the impact? (High / Medium / Low)" (AskUserQuestion per risk)

Score = Probability × Impact:
- H×H = Critical
- H×M or M×H = High
- M×M or H×L or L×H = Medium
- M×L or L×M = Low
- L×L = Negligible

---

## Step 3 — Mitigation per high/critical risk

For every Critical or High risk only:

**Q5:** "For '[risk name]': what is the mitigation plan? (prevent / reduce probability / reduce impact / accept)" (free text)

**Q6:** "For '[risk name]': what is the trigger — how will you know this risk is activating?" (free text)

Low and Medium risks: document without mitigation detail unless user volunteers one.

---

## Document Generation

```markdown
# Risk Register

**Project:** [name]
**Date:** [today]

## Risk Matrix

| # | Risk | Category | Probability | Impact | Score | Mitigation |
|---|------|----------|-------------|--------|-------|-----------|
| 1 | [risk] | Technical | H/M/L | H/M/L | Critical/High/Medium/Low | [plan or "Accept"] |
| [...] | | | | | | |

Score: H×H=Critical, H×M or M×H=High, M×M=Medium, L×L=Negligible

## Critical and High Risks

### [Risk name] — [Score]

**Description:** [what the risk is]
**Source:** [which doc surfaced this, or "identified in interview"]
**Probability:** [H/M/L] — [brief rationale]
**Impact:** [H/M/L] — [what breaks if this happens]
**Trigger:** [how you'd know it's activating]
**Mitigation:** [plan]

---

[Repeat for each Critical/High risk]

## Medium and Low Risks

| Risk | Probability | Impact | Score | Note |
|------|-------------|--------|-------|------|
| [risk] | M/L | M/L | Medium/Low | [brief note or "Accept"] |

## Open Questions

[Risks that are actually unknown — need resolution before they can be rated]
```

## File Output

Write to `06_decisions/risk_docs.md`. Create folder if missing.

## Quality Check Before Writing

- Every Critical and High risk has a mitigation plan and trigger
- Risk count not hardcoded — document however many exist
- Each risk has a source (which doc, which assumption)
- "Accept" is a valid mitigation for Low risks — don't force mitigation plans where they don't make sense
