---
name: frontend-architecture
description: Use when creating a frontend architecture document. Defines framework, state management, routing, component structure, and UI conventions. Writes to 04_tech/.
---

# Frontend Architecture

Interview the user to define frontend architecture decisions. Write to `04_tech/frontend_architecture.md`.

## Process

```
Scan context → Framework → State management → Routing → Component structure → Styling → Write
```

## Step 0 — Scan context

Read `03_design/ux_spec.md` if exists (screens, flows, interaction patterns).
Read `04_tech/backend_architecture.md` if exists (API style affects frontend data fetching).

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What frontend framework/platform?" (options: React (web) / React Native (mobile) / Vue / Next.js / Flutter / Not decided)

**Q2:** "How will state be managed?" (options: Local component state only / Context/Zustand/Pinia / Redux/Vuex / Server state (React Query/SWR) / Not decided)

**Q3:** "How will routing work?" (free text or "Not decided")
Example: "File-based routing (Next.js)", "React Router v6 with protected routes", "Tab-based navigation (React Native)"

**Q4:** "What is the component organization strategy?" (options: Feature folders / Atomic Design / Domain-based / Flat / Not decided)

**Q5:** "How will styling be handled?" (options: Tailwind CSS / CSS Modules / Styled Components / Native styles (mobile) / Not decided)

**Q6:** "How will the frontend communicate with the backend?" (options: REST fetch/axios / GraphQL client / tRPC / SDK generated from API / Not decided)

**Q7:** "Are there any offline or caching requirements?" (free text)

**Q8:** "What are the top 3 UI performance or quality requirements?" (free text)

## Document Generation

```markdown
# Frontend Architecture

**Project:** [name]
**Date:** [today]

## Stack

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Framework | [Q1] | [reason] |
| State management | [Q2] | [reason] |
| Routing | [Q3] | [reason] |
| Component structure | [Q4] | [reason] |
| Styling | [Q5] | [reason] |
| Backend communication | [Q6] | [reason] |

## Component Structure

[Q4 — describe folder structure and naming convention]

```
src/
  features/
    [feature-name]/
      components/
      hooks/
      [feature].store.ts (if state)
  shared/
    components/
    hooks/
  pages/ (or screens/ for mobile)
```

## State Management Decisions

[Q2 — what lives where: server state vs local state vs global state]

## Offline and Caching

[Q7 — if applicable]

## Quality Requirements

1. [Q8 requirement 1]
2. [Q8 requirement 2]
3. [Q8 requirement 3]

## Open Decisions

[Any undecided items that will be resolved when work starts]
```

## File Output

Write to `04_tech/frontend_architecture.md`. Create folder if missing.
