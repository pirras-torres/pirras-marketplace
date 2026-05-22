---
name: risk-docs
description: Use when creating a risk register for a software project. Identifies technical, product, and delivery risks with mitigation strategies. Writes to 06_decisions/.
---

# Risk Documentation

Interview the user to identify and document risks. Write to `06_decisions/risk_docs.md`.

## Process

```
Scan context → Technical risks → Product risks → Delivery risks → Mitigation → Write
```

## Step 0 — Scan context

Read existing architecture and product docs. Extract open decisions and constraints — these are risk candidates.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What technical decisions haven't been made yet that could block progress?" (free text)

**Q2:** "What assumptions about user behavior could be wrong?" (free text)
Example: "Users will capture data manually", "Users have one primary account"

**Q3:** "What external dependencies could fail or be unavailable?" (free text)
Example: "Bank API", "Third-party library", "App store approval"

**Q4:** "What would cause this project to fail completely?" (free text — 2-3 answers)

**Q5:** "For the top 3 risks, what is the mitigation plan?" (free text — address each risk from Q1-Q4)

## Document Generation

```markdown
# Risk Register

**Project:** [name]
**Date:** [today]

## Risk Matrix

| # | Risk | Category | Probability | Impact | Score | Mitigation |
|---|------|----------|-------------|--------|-------|-----------|
| 1 | [risk] | Technical | H/M/L | H/M/L | H/M/L | [plan] |
| 2 | [risk] | Product | H/M/L | H/M/L | H/M/L | [plan] |
| [...] | | | | | | |

Score = Probability × Impact (H×H = Critical, H×M or M×H = High, etc.)

## Technical Risks

### [Risk 1]
**Description:** [Q1]
**Trigger:** [what would activate this risk]
**Mitigation:** [plan from Q5]

---

## Product Risks

### [Risk 1]
**Assumption at risk:** [Q2]
**Trigger:** [when we'd know this assumption failed]
**Mitigation:** [plan]

---

## Delivery Risks

### [Risk 1]
**Dependency:** [Q3]
**Mitigation:** [plan]

---

## Open Questions (unresolved at doc date)

[List of open questions from Q4 that must be resolved before building]
```

## File Output

Write to `06_decisions/risk_docs.md`. Create folder if missing.
