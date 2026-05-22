---
name: slices-discovery
description: Use when breaking down a backlog into vertical slices for incremental delivery. Defines thin slices that deliver end-to-end value. Writes to 04_tech/.
---

# Slices Discovery

Help the user break features into thin vertical slices — each slice delivers end-to-end value from UI to data layer. Write to `04_tech/slices_discovery.md`.

## What Is a Vertical Slice

A vertical slice cuts through all layers (UI → logic → data) to deliver ONE working capability. It is NOT a layer-by-layer task list.

Bad: "Build the accounts screen", "Build the accounts API", "Build the accounts table" (horizontal)
Good: "User can see their account balance with one account and one manual transaction" (vertical)

## Process

```
Scan context → Identify slices → Per slice: layers + scope + acceptance → Order → Write
```

## Step 0 — Scan context

Read `05_scrum/backlog.md` if exists. Extract epics and must-have stories.
Read `03_design/ux_spec.md` if exists. Extract key flows.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "Pick one epic or feature to slice. Which one?" (free text)

**Q2:** "What is the thinnest version of [feature] that delivers real value to a real user?" (free text)
This is Slice 1. Push the user toward minimum viable slices.

**Q3:** "What does Slice 1 include in each layer?"
- UI: [what the user sees and can do]
- Logic: [what rules/calculations run]
- Data: [what gets stored/read]
(ask this as one free-text question)

**Q4:** "What does Slice 1 NOT include? (what is deferred to later slices)" (free text)

**Q5:** "What is Slice 2? What additional value does it add beyond Slice 1?" (free text)
Repeat Q3-Q4 for Slice 2. Continue until user says "that's all" or reaches Slice 5.

**Q6:** "What is the order slices must be built in? (any technical dependencies between slices?)" (free text)

## Document Generation

```markdown
# Slices Discovery

**Project:** [name]
**Feature:** [Q1]
**Date:** [today]

## Slicing Principle

Each slice delivers working software end-to-end. No slice is "just backend" or "just frontend".

---

## Slice 1: [Name — describe the value delivered]

**Value delivered:** [What a user can actually do after this slice]

**Scope:**
- UI: [what is included]
- Logic: [what rules run]
- Data: [what is stored/read]

**Excluded (deferred):** [Q4]

**Acceptance:** [How to verify this slice works end-to-end]

---

[Repeat per slice]

## Build Order

1. Slice 1 → [reason]
2. Slice 2 → [reason]
3. [...]

## Dependencies

[Q6 — technical dependencies between slices]
```

## File Output

Write to `04_tech/slices_discovery.md`. Create folder if missing. One file per feature/epic is acceptable — append if file already exists.
