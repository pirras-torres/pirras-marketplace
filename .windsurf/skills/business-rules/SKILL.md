---
name: business-rules
description: Use when creating a Business Rules document. Defines the explicit constraints, validations, and policies the system must enforce. Writes to 02_business/.
---

# Business Rules

Interview the user to define business rules per domain area. Write to `02_business/business_rules.md`.

## Process

```
Scan context → Per subdomain: rules → Validation rules → State transition rules → Write
```

## Step 0 — Scan context

Read `02_business/domain_model.md` if exists. Extract: subdomains and invariants. Tell the user what you found and use it as the starting point.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "Which subdomains have the most critical business rules?" (free text — user names 2-5 subdomains)

For each subdomain the user names, ask:

**Q2:** "What rules govern [subdomain name]? List them as 'must', 'cannot', 'only when', or 'always'." (free text)

Example format:
- A withdrawal CANNOT exceed available balance
- A purchase MUST be associated with exactly one account
- A credit payment ONLY applies to a credit account

**Q3:** "What data validations exist? (required fields, formats, ranges, uniqueness)" (free text)

**Q4:** "Are there state machines? (things that have lifecycle states with rules about transitions)" (free text)
Example: "An Apartado can only be ACTIVE or DISSOLVED. It transitions to DISSOLVED only when fully consumed."

**Q5:** "What are the top 3 rules that, if violated, would corrupt data or break user trust?" (free text)
These become the CRITICAL rules — highlighted in the document.

## Document Generation

```markdown
# Business Rules

**Project:** [name]
**Date:** [today]

## 1. Critical Rules (must never be violated)

1. [Q5 rule 1]
2. [Q5 rule 2]
3. [Q5 rule 3]

## 2. Rules by Subdomain

### [Subdomain 1]

- [rule 1]
- [rule 2]
- [...]

### [Subdomain 2]

- [...]

## 3. Validation Rules

| Field | Validation | Error message |
|-------|-----------|---------------|
| [field] | [rule] | [message] |

## 4. State Transitions

### [Entity with states]

**States:** [list states]

**Transitions:**
- [State A] → [State B] when: [condition]
- [State B] → [State C] when: [condition]
- [State B] → [State A] NEVER (irreversible)
```

## File Output

Write to `02_business/business_rules.md`. Create folder if missing.
