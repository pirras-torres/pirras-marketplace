---
name: data-model
description: Use when creating a Data Model document. Derives entities from the domain model, then asks about storage details per entity. Writes to 02_business/.
---

# Data Model

Define the persistence model. Derives entity list from domain model — doesn't ask again for what's known.

## Process

```
Read domain model + business rules → Present entity list → Confirm which need storage
→ Per entity: fields + types → Relationships → Conventions → Write
```

## Step 0 — Read existing docs (required)

Read `02_business/domain_model.md`. Extract:
- All entities with their attributes
- All relationships
- States if defined

Read `02_business/business_rules.md` if exists. Extract:
- Validation rules (these become field constraints)
- State transition rules (these become state field options)

**If domain model doesn't exist:** tell user to run `kick-development:domain-model` first.

Tell user:
> "I found these entities in the domain model: [list]. I'll create a table for each. Some entities may be transient (no storage needed) — let me know which."

---

## Step 1 — Storage scope

**Q1:** "Which entities from the domain model need persistent storage? Are any transient (calculated, in-memory only)?" (free text or "All need storage")

Remove transient entities from the table list.

---

## Step 2 — Storage technology

**Q2:** "What type of storage?" (AskUserQuestion options: Relational SQL / Document NoSQL / Both / Not decided yet)

---

## Step 3 — Per entity: field details

For each entity that needs storage, present what the domain model already defines (attributes) and ask for storage specifics:

**Q3:** "For [Entity]: the domain model defines attributes [list]. What are the data types, constraints, and any additional fields not in the domain model?" (free text)

Example guidance: "id (UUID, PK), amount (DECIMAL 10,2, NOT NULL, > 0), account_id (UUID, FK → accounts), created_at (TIMESTAMP, NOT NULL)"

For each validation rule from business_rules.md that applies to this entity, pre-fill it as a constraint.

**Q4:** "For [Entity]: what are the most common read queries? (affects indexes)" (free text)
Example: "Find all transactions by account, ordered by date" → index on account_id + created_at

---

## Step 4 — Conventions

**Q5:** "Soft deletes or physical deletes?" (AskUserQuestion options: Soft delete (deleted_at) / Physical delete / Mixed — depends on entity / Not decided)

**Q6:** "Is data isolated per user, per organization, or shared?" (options: Per user / Per organization / Shared / Not applicable)

**Q7:** "What is the primary key convention?" (options: UUID / Auto-increment integer / Other)

---

## Document Generation

```markdown
# Data Model

**Project:** [name]
**Storage:** [Q2]
**Date:** [today]
**Source:** Derived from `02_business/domain_model.md`

## Conventions

- **Primary keys:** [Q7]
- **Soft deletes:** [Q5]
- **Tenancy:** [Q6]
- **Timestamps:** all tables include `created_at`, `updated_at` (NOT NULL)
[deleted_at if soft delete]

## Tables

### [entity_name]

| Field | Type | Constraints | Notes |
|-------|------|-------------|-------|
| id | [type] | PRIMARY KEY | |
| [field from domain model] | [type] | [from validation rules] | |
| created_at | TIMESTAMP | NOT NULL | |
| updated_at | TIMESTAMP | NOT NULL | |
[| deleted_at | TIMESTAMP | NULLABLE | Soft delete |]

**Indexes:**
- `[field(s)]` — reason: [from Q4 query pattern]

**Domain model ref:** attributes match `02_business/domain_model.md#[Entity]`

---

[Repeat per table]

## Relationships

| From | Type | To | Foreign key |
|------|------|----|-------------|
| [table_a] | has many | [table_b] | table_b.table_a_id |

## Validation Constraints (from business_rules.md)

| Table.Field | Constraint | Source rule |
|------------|-----------|-------------|
| [table.field] | CHECK (> 0) | [rule name] |
```

## File Output

Write to `02_business/data_model.md`. Create folder if missing.

## Quality Check Before Writing

- Every entity in storage scope has a table
- Every validation rule from business_rules.md has a corresponding constraint
- Every field has explicit type and NOT NULL or NULLABLE
- Indexes address the query patterns described
