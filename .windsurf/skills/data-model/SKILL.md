---
name: data-model
description: Use when creating a Data Model document. Defines tables, fields, types, and relationships for the system's persistence layer. Writes to 02_business/.
---

# Data Model

Interview the user to define the persistence data model. Write to `02_business/data_model.md`.

## Process

```
Scan context → Storage type → Per entity: table, fields, types → Relationships → Indexes → Write
```

## Step 0 — Scan context

Read `02_business/domain_model.md` if exists. Extract entities and relationships. Use them as the starting point for tables.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What type of storage will you use?" (AskUserQuestion options: Relational SQL / Document (NoSQL) / Both / Not decided yet)

**Q2:** "Which domain entities map to stored data? (Some entities may be transient — don't need storage)" (free text)

For each entity the user confirms needs storage, ask:

**Q3:** "What are the fields for [Entity]? List name and type." (free text)
Example: "id (UUID), amount (decimal), created_at (timestamp), account_id (UUID foreign key)"

**Q4:** "What are the most common queries against [Entity]? (affects what indexes to define)" (free text)

**Q5:** "Are there any soft deletes? (logical deletion instead of physical)" (options: Yes — use deleted_at / No — physical delete / Mixed)

**Q6:** "Any multi-tenancy? (is data isolated per user, organization, or shared?)" (options: Per user / Per organization / Shared / Not applicable)

## Document Generation

```markdown
# Data Model

**Project:** [name]
**Storage:** [Q1]
**Date:** [today]

## Tables

### [entity_name]

| Field | Type | Constraints | Notes |
|-------|------|-------------|-------|
| id | UUID | PRIMARY KEY | |
| [field] | [type] | [NOT NULL / FK / etc.] | [note] |
| created_at | TIMESTAMP | NOT NULL | |
| updated_at | TIMESTAMP | NOT NULL | |
[| deleted_at | TIMESTAMP | NULLABLE | Soft delete |]

**Indexes:**
- [field] — reason: [Q4]

---

[Repeat per table]

## Relationships

| From | Relationship | To | Foreign key |
|------|-------------|-----|------------|
| [table_a] | has many | [table_b] | table_b.table_a_id |
| [...] | [...] | [...] | [...] |

## Conventions

- [Soft delete strategy if applicable]
- [Multi-tenancy strategy if applicable]
- [ID type convention]
- [Timestamp convention]
```

## File Output

Write to `02_business/data_model.md`. Create folder if missing.
