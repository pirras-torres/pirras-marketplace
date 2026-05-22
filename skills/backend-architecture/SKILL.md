---
name: backend-architecture
description: Use when creating a backend architecture document. Reads existing project docs to determine what decisions matter for this specific project, then interviews accordingly. Writes to 04_tech/.
---

# Backend Architecture

Adaptive skill. Reads existing project documents first, determines which architectural decisions are relevant to THIS project, then interviews the user on those specific decisions.

No fixed template — sections are derived from what the project needs.

## Process

```
Scan all docs → Identify relevant decision areas → Interview on those areas only
→ Generate doc with sections appropriate to this project → Write
```

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Deep context scan

Read ALL of the following that exist:

| Document | What to extract |
|----------|----------------|
| `docs/01_product/01_prd.md` | Scale hints, user type, offline needs, performance expectations |
| `docs/01_product/03_product_principles.md` | Technical implications of each principle |
| `docs/02_business/domain_model.md` | Entities, subdomains, invariants — shapes API structure |
| `docs/02_business/business_rules.md` | Rules that must be enforced server-side |
| `docs/02_business/data_model.md` | Tables, relationships, query patterns |
| `docs/03_design/ux_spec.md` | Flows that need API support, real-time needs, offline flows |
| `docs/05_scrum/discovery/S*.md` | Slice scopes — what backend work is coming first |

After reading, tell the user:
> "I found [list of docs]. Based on these, the decisions that matter most for this project's backend are: [list decisions you identified]. I'll focus the interview on these."

Then ask: "Is there anything I missed or a concern I should add?" (free text)

## Decision Area Detection

Based on what you found, determine which of these areas need decisions:

**Always ask:**
- Stack (language, framework)
- API style
- Authentication

**Ask if data_model.md exists or entities found:**
- Data access patterns and ORM strategy
- Query performance risks (N+1, large joins)

**Ask if business_rules.md has complex invariants:**
- Where rules are enforced (DB constraints vs application layer vs both)
- Transaction strategy

**Ask if ux_spec.md has real-time features (live updates, notifications):**
- Real-time strategy (websockets, polling, SSE)

**Ask if PRD suggests mobile or offline:**
- Sync strategy
- Offline-first vs online-required

**Ask if multiple subdomains in domain model:**
- Internal module/service boundaries
- How subdomains map to code structure

**Ask if slices exist:**
- What the first slice needs from the backend (informs what to build first)

**Ask if no existing docs:**
- Fall back to standard questions: stack, API style, auth, deployment, DB, structure

## Interview

Ask ONLY the questions relevant to this project based on Step 0. Use AskUserQuestion. One question at a time.

For each decision area identified, ask the specific question. Examples:

**Stack:**
"What is the backend language and framework?" (free text or "not decided")

**API style:**
"What API style?" (options: REST / GraphQL / tRPC / gRPC / Not decided)

**Auth:**
"How will authentication work?" (options: JWT / Session / OAuth/SSO / Magic link / Not decided)
Follow up if needed: "Any authorization model? (roles, per-resource permissions, none)"

**Data access (if data model exists):**
"For [Entity from data_model], what are the most frequent read patterns? Any risk of large result sets?" (free text)

**Rule enforcement (if complex business rules found):**
"[Rule X] from business_rules.md — enforced at DB level (constraint), application level, or both?" (per critical rule)

**Real-time (if ux_spec suggests it):**
"[Flow X] in UX spec seems to need live updates. How should this work?" (options: Polling / WebSockets / Server-Sent Events / Not needed / Not decided)

**Module boundaries (if multiple subdomains):**
"How do the [subdomain list] subdomains map to code structure?" (options: Single module / Feature folders / Separate packages / Not decided)

**Error handling:**
"What is the error response format? How does the API communicate failures to clients?" (free text)

**Deployment:**
"How will the backend be deployed?" (options: Single server / Serverless / Containers / Not decided)

## Document Generation

Generate sections based on what was actually discussed. Do not include empty sections.

```markdown
# Backend Architecture

**Project:** [name]
**Date:** [today]

## Context

[Brief summary of what existing docs informed this architecture — which docs were read, key constraints found]

## Stack Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Language/Framework | [answer] | [why, linked to project context] |
| API style | [answer] | [why] |
| Auth | [answer] | [why] |
| Deployment | [answer] | [why] |
| [other decisions made] | | |

## Internal Structure

[How the backend is organized internally — derived from subdomain analysis if available]

## Data Access

[Only if data_model.md existed — key patterns, ORM choice, query risks identified]

## Business Rule Enforcement

[Only if complex rules found — where each critical rule is enforced and why]

## API Design Conventions

[Error format, versioning, pagination, naming — based on API style chosen]

## [Real-time / Sync] (only if applicable)

[Strategy and rationale — only if ux_spec or PRD indicated this is needed]

## First Slice Backend Needs

[Only if slices exist — what the backend must deliver for S1]

## Open Decisions

[Questions that came up but weren't resolved — with context for when to decide]
```

## File Output

Write to `docs/04_tech/backend_architecture.md`. Create folder if missing.
