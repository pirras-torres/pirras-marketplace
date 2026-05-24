---
name: frontend-architecture
description: Use when creating a frontend architecture document. Reads existing project docs to determine what decisions matter for this specific project, then interviews accordingly. Writes to 04_tech/.
---

# Frontend Architecture

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
| `docs/01_product/01_prd.md` | Platform hints, user type, offline needs, performance expectations |
| `docs/01_product/03_product_principles.md` | Technical implications for UI/UX tradeoffs |
| `docs/02_business/domain_model.md` | Entities the UI must represent, state complexity |
| `docs/02_business/business_rules.md` | Rules the frontend must enforce or communicate |
| `docs/03_design/ux_spec.md` | Screens, flows, navigation model, interaction rules |
| `docs/03_design/ui_spec.md` | Design system, component library, styling approach |
| `docs/04_tech/backend_architecture.md` | API style, auth method — shapes data fetching |
| `docs/05_scrum/discovery/S*.md` | First slice scope — what frontend must deliver first |

After reading, tell the user:
> "I found [list of docs]. Based on these, the decisions that matter most for this project's frontend are: [list decisions identified]. I'll focus the interview on these."

Then ask: "Is there anything I missed or a concern I should add?" (free text)

## Decision Area Detection

Based on what you found, determine which areas need decisions:

**Always ask:**
- Framework/platform
- State management approach

**Ask if ux_spec.md exists with defined screens:**
- Routing strategy (how navigation from ux_spec maps to code)
- How screens map to components/pages

**Ask if ui_spec.md exists with a design system:**
- How the design system integrates (import tokens, use component lib, custom)

**Ask if domain_model.md has complex entities or many relationships:**
- Server state vs local state split
- How domain entities map to frontend data structures

**Ask if backend_architecture.md exists:**
- Data fetching pattern that matches the API style (REST → React Query/SWR, GraphQL → Apollo/urql, tRPC → native)
- Auth integration (how JWT/session is stored and sent)

**Ask if business_rules.md has frontend-enforceable rules:**
- Which rules are validated client-side (UX feedback) vs backend-only (source of truth)

**Ask if ux_spec.md has offline flows or PRD mentions offline:**
- Offline strategy (cache, sync, conflict resolution)

**Ask if ux_spec.md has real-time features:**
- How real-time updates flow into the UI (push to store, optimistic updates, polling)

**Ask if multiple distinct screen types (forms, dashboards, detail views):**
- Error and loading state pattern per screen type

**Ask if no existing docs:**
- Fall back to: framework, state management, routing, styling, data fetching

## Interview

Ask ONLY the questions relevant to this project based on Step 0. One question at a time with AskUserQuestion.

**Framework:**
"What frontend framework/platform?" (options: React web / React Native / Next.js / Vue / Flutter / Not decided)

**State management:**
"How will state be managed?" (options derived from framework choice)
- If React: Local state / Zustand / Redux / Server state only (React Query) / Not decided
- If Vue: Pinia / Vuex / Local / Not decided
- If React Native: Same as React options

**Routing (if ux_spec has navigation model):**
"The UX spec defines [navigation model]. How does this map to routing in code?" (free text)

**Design system integration (if ui_spec exists):**
"ui_spec defines [tokens/components]. How does the frontend consume these?" (options: CSS variables / JS tokens / Component lib import / Custom implementation / Not decided)

**Data fetching (if backend_architecture exists):**
"The backend uses [API style]. What data fetching pattern?" (options matched to API style)

**Auth integration (if auth method known):**
"Auth uses [method]. How does the frontend store and send credentials?" (free text)

**Client-side rule enforcement (if complex rules found):**
"[Rule X] — should the frontend validate this client-side for UX feedback, or rely solely on backend?" (per relevant rule)

**Error/loading states (if multiple screen types):**
"What is the standard pattern for loading and error states across screens?" (free text)

**Offline (if applicable):**
"What is the offline strategy?" (options: Full offline / Cache-then-network / Online required / Not decided)

**File structure:**
"How should the project be structured?" (options: Feature folders / Atomic Design / Domain-based / Flat / Not decided)

## Document Generation

Generate sections based on what was actually discussed. Do not include empty sections.

```markdown
# Frontend Architecture

**Project:** [name]
**Platform:** [framework/platform]
**Date:** [today]

## Context

[Brief summary of what existing docs informed this architecture — key constraints, screen count, domain complexity, API style]

## Stack Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Framework | [answer] | [why, linked to project context] |
| State management | [answer] | [why] |
| Data fetching | [answer] | [why] |
| Styling | [from ui_spec or answered] | [why] |
| [other decisions] | | |

## File Structure

[Folder structure derived from framework + feature complexity found in ux_spec]

```
src/
  [structure based on decisions made]
```

## State Architecture

[What lives where: server state vs UI state vs global state — based on domain entities and screen complexity]

## Routing

[Only if ux_spec navigation model was found — how it maps to code]

## Design System Integration

[Only if ui_spec exists — how tokens and components are consumed]

## Data Fetching Patterns

[How API calls are made, cache strategy, loading/error handling — based on backend API style]

## Client-Side Rule Enforcement

[Only if relevant rules found — which rules validate client-side and which defer to backend]

## [Offline / Real-time] (only if applicable)

[Strategy and rationale — only if relevant]

## First Slice Frontend Needs

[Only if slices exist — what frontend must deliver for S1]

## Open Decisions

[Unresolved questions with context for when to decide]
```

## File Output

Write to `docs/04_tech/frontend_architecture.md`. Create folder if missing.
