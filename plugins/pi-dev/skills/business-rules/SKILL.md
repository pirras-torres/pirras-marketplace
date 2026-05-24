---
name: business-rules
description: Use when creating a Business Rules document. Starts from invariants already defined in the domain model, then expands with additional rules per subdomain. Writes to 02_business/.
---

# Business Rules

Define business rules per domain area. Starts from what's already in the domain model — doesn't ask again for what's known.

## Process

```
Read domain model → Present known invariants → Expand per subdomain
→ Validation rules → State transitions → Write
```

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Read domain model (required)

Read `docs/02_business/domain_model.md`. Extract:
- All invariants from section 6
- All subdomains with their responsibilities
- Entities and their states (if defined)

**If domain model doesn't exist:** tell user to run `kick-development:domain-model` first. Business rules need the domain model as foundation.

Tell user:
> "I found [N] invariants in the domain model: [list them]. These will be included as Critical Rules. Now I'll ask about additional rules per subdomain."

---

## Step 1 — Confirm and extend critical rules

**Q1:** "The domain model defines these invariants: [list]. Are any of these wrong or outdated? Anything to add?" (free text or "All correct")

---

## Step 2 — Per subdomain rules

For each subdomain found in the domain model, ask:

**Q2:** "What additional rules govern [subdomain name] beyond the invariants already listed? Use: 'must', 'cannot', 'only when', 'always'." (free text or "None beyond invariants")

Ask per subdomain. Skip subdomains where user answers "None."

---

## Step 3 — Validation rules

**Q3:** "What data validations exist? (required fields, formats, value ranges, uniqueness constraints)" (free text)
Example: "Amount must be > 0. Account name max 100 chars. Email must be unique per user."

---

## Step 4 — State transitions

If the domain model defined entities with states, ask for each:

**Q4:** "Entity [X] has states [list from domain model]. What are the allowed transitions and conditions for each?" (free text)
Example: "Apartado: Active → Dissolved when fully consumed. Cannot go back to Active once Dissolved."

If no states in domain model: skip this step.

---

## Step 5 — Frontend vs backend enforcement

**Q5:** "Which critical rules should the frontend enforce for UX feedback (not just the backend)?" (free text or "None — backend only")

This determines which rules need client-side validation vs. server-only enforcement.

---

## Document Generation

```markdown
# Business Rules

**Project:** [name]
**Date:** [today]
**Source:** Derived from `docs/02_business/domain_model.md` + additional rules

## 1. Critical Rules (must never be violated)

These rules, if broken, corrupt data or destroy user trust. Enforced at all layers.

1. [Invariant from domain model + Q1 additions]
2. [...]

## 2. Rules by Subdomain

### [Subdomain 1]

- [rule — phrased as must/cannot/only when/always]
- [...]

### [Subdomain 2]

- [...]

## 3. Validation Rules

| Field / Entity | Validation | Error message |
|----------------|-----------|---------------|
| [field] | [rule] | [message shown to user] |

## 4. State Transitions

### [Entity with states]

**States:** [list]

**Allowed transitions:**
- [State A] → [State B]: when [condition]
- [State B] → [State C]: when [condition]
- [State B] → [State A]: **never** (irreversible)

## 5. Frontend vs Backend Enforcement

| Rule | Backend | Frontend |
|------|---------|----------|
| [rule] | ✅ always | ✅ UX feedback |
| [rule] | ✅ always | ❌ backend only |
```

## File Output

Write to `docs/02_business/business_rules.md`. Create folder if missing.

## Quality Check Before Writing

- Every invariant from domain model appears in Critical Rules
- Rules use enforcement language (must/cannot/only when), not description language
- Validation rules have user-facing error messages
- State transitions explicitly mark irreversible ones
