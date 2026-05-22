---
name: backend-architecture
description: Use when creating a backend architecture document. Defines the technical stack, API design, data access patterns, and service structure. Writes to 04_tech/.
---

# Backend Architecture

Interview the user to define backend architecture decisions. Write to `04_tech/backend_architecture.md`.

## Process

```
Scan context → Stack decisions → API design → Data access → Auth → Non-functional → Write
```

## Step 0 — Scan context

Read `02_business/domain_model.md` and `02_business/data_model.md` if they exist.
Read `01_product/01_prd.md` for scale and non-functional hints.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What is the primary backend language/framework?" (free text or "not decided")

**Q2:** "What API style will you use?" (options: REST / GraphQL / tRPC / gRPC / Not decided)

**Q3:** "How will the backend be deployed?" (options: Single server / Serverless functions / Containers / Not decided)

**Q4:** "What is the database?" (free text — mention type and specific tech)

**Q5:** "How will authentication work?" (options: JWT tokens / Session-based / OAuth/SSO / Magic link / Not decided)

**Q6:** "How is the backend structured internally?" (options: Monolith / Modular monolith / Microservices / Not decided)

**Q7:** "What are the top 3 non-functional requirements?" (free text)
Example: "Response < 200ms for reads", "Offline-capable", "Single user — no multi-tenancy needed"

**Q8:** "What are the riskiest technical decisions you haven't made yet?" (free text)

## Document Generation

```markdown
# Backend Architecture

**Project:** [name]
**Date:** [today]

## Stack

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Language/Framework | [Q1] | [reason] |
| API style | [Q2] | [reason] |
| Deployment | [Q3] | [reason] |
| Database | [Q4] | [reason] |
| Auth | [Q5] | [reason] |
| Structure | [Q6] | [reason] |

## Internal Structure

[Q6 — describe how code is organized: modules, layers, boundaries]

## API Design Conventions

[Derived from Q2 — naming, versioning, error format, pagination]

## Data Access Patterns

[From domain model — how entities are read/written, what queries are most frequent]

## Non-Functional Requirements

1. [Q7 requirement 1] — [how it's addressed architecturally]
2. [Q7 requirement 2]
3. [Q7 requirement 3]

## Open Decisions

[Q8 — undecided items with context for when/how to decide]
```

## File Output

Write to `04_tech/backend_architecture.md`. Create folder if missing.
