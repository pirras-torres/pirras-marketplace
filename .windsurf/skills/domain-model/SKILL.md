---
name: domain-model
description: Use when creating the domain model document for a software project. Defines the ubiquitous language, entities, relationships, and business rules. Writes to 02_business/.
---

# Domain Model

Interview the user to define the domain language, entities, relationships, and subdomains. Write results to `02_business/domain_model.md`.

## Process

```
Scan context → Domain context → Ubiquitous language → Entities → Relationships
→ Subdomains → Business rules summary → Generate doc → Write to disk
```

## Step 0 — Scan context

Before asking anything:
- Read `01_product/01_prd.md` if it exists. Extract: product name, problem description, and target user.
- If PRD exists, tell the user: "I found the PRD for [product name]. I'll use it as context."
- If no PRD exists, ask for a brief description of what the software does (free text, 2-3 sentences).

## Step 1 — Domain context

**Q1:** "What is the main responsibility of this domain in one sentence? Example: 'Represents personal financial information so the user understands availability, debt, and payments.'" (free text)

**Q2:** "What does this domain NOT do? (what it explicitly avoids)" (free text)
Example: "Does not connect to banks, does not give financial advice, does not automate reconciliation."

## Step 2 — Subdomains

**Q3:** "List the main areas of concern (subdomains) in this system. Example for a finance app: accounts, movements, payments, debt, budgets." (free text — expect comma-separated list)

For each subdomain the user lists, ask one follow-up:
"What is the responsibility of [subdomain name] in one sentence?"

Limit to max 10 subdomains. If user lists more, ask them to group related ones.

## Step 3 — Ubiquitous language

**Q4:** "List the most important terms (5-15) that have a precise meaning in this domain. These are words that both the team and users would use." (free text)

For each term, ask:
"Define [term] in one sentence as it is used in this system."

This builds the ubiquitous language table. Focus on terms that:
- Could be confused with common usage
- Have a specific technical meaning in this domain
- Appear in user-facing features

## Step 4 — Core entities

**Q5:** "What are the main entities (things) in this system? List them." (free text — expect list)

For each entity, ask:
- "What does a [Entity] represent?"
- "What are its key attributes? (2-5 most important)"
- "What states can it be in? (if applicable)"

## Step 5 — Key relationships

**Q6:** "How do the entities relate to each other? List the most important relationships." (free text)

Example format the user can follow: "A User has many Accounts. An Account has many Movements. A Movement belongs to one Account."

Ask: "Are there any containment rules? (e.g., 'An Apartado must always belong to an Account')" (free text)

## Step 6 — Invariants and constraints

**Q7:** "What are the most critical business rules or invariants? These are rules the system must NEVER break." (free text)

Example: "Available balance can never go below zero after a withdrawal.", "A credit card payment can only be made from a debit or cash account."

List 3-10 invariants. These become the foundation for the business rules document.

## Document Generation

Generate `02_business/domain_model.md`:

```markdown
# Domain Model

**Project:** [name]
**Status:** Foundational domain model
**Date:** [today]

## 1. Purpose

[Domain context from Q1]

**What this domain does NOT do:** [Q2]

**Source documents:**
- [Link to PRD if exists]

## 2. Domain Context

**[Domain Name]**

Responsibility: [Q1]

Subdomains:
- [subdomain 1]: [responsibility]
- [subdomain 2]: [responsibility]
- [...]

## 3. Ubiquitous Language

| Term | Definition |
|------|-----------|
| [Term 1] | [Definition] |
| [Term 2] | [Definition] |
| [...] | [...] |

## 4. Core Entities

### [Entity 1]
[Description]

Key attributes:
- [attribute 1]
- [attribute 2]

States: [if applicable]

### [Entity 2]
[...]

## 5. Key Relationships

- [Entity A] — [relationship] — [Entity B]
- [...]

**Containment rules:**
- [rule if any]

## 6. Invariants

1. [Invariant 1]
2. [Invariant 2]
3. [...]
```

## File Output

- Create `02_business/` folder if missing
- Write to `02_business/domain_model.md`
- After writing, offer to also create `02_business/business_rules.md` with expanded rules using `kick-development:business-rules`

## Quality Check Before Writing

- Ubiquitous language has at least 5 terms
- Each entity has a definition and at least 2 attributes
- Invariants are phrased as constraints ("must", "cannot", "never"), not features
- Subdomains cover all major areas mentioned in the PRD
