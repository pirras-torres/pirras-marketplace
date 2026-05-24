---
name: guide
description: Use when starting, continuing, or resuming work on a software project. Reads project memory and doc state, determines what phase the project is in, and suggests the concrete next action. Run at the start of every session.
---

# Development Guide — Orchestrator

Active orchestrator. Reads project state, tells you exactly what to do next, invokes the right skill, and updates memory after each action.

**Run this at the start of every session.** It picks up where you left off.

## Core Concept: The Incremental Cycle

```
FOUNDATION (once)
  Product docs → Business docs → Design docs

ARCHITECTURE (once, updated when decisions change)
  Backend + Frontend → DoR + DoD → Risk Register

SLICE CYCLE (repeats per slice)
  Discovery S# → Backlog S# → Sprint Planning
  → BUILD → Sprint Review → [next slice or update docs]
```

Foundation and Architecture happen once. The Slice Cycle repeats until the product is done.

---

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Load project memory

Check if `project_memory.md` exists in the project root:

```bash
cat project_memory.md 2>/dev/null || echo "NO_MEMORY"
```

**If memory exists:** read it fully. Extract: current phase, active slice, sprint state, blockers, last action.  
**If no memory:** this is a new project. Create fresh memory (see Memory Format below). Phase = Foundation.

---

## Step 1 — Verify doc state

Run:
```bash
find . -path "*/docs/*" -type f -name "*.md" | grep -E "(0[1-9]_|discovery/S|sprints/sprint)" | sort
```

Cross-reference with memory. If memory says "Foundation complete" but PRD is missing, flag the discrepancy and correct memory.

---

## Step 2 — Determine current phase

### FOUNDATION phase
**Condition:** Any of these missing:
- `docs/01_product/01_prd.md`
- `docs/02_business/domain_model.md`
- `docs/03_design/ux_spec.md`

**Action:** Show which foundation docs are missing. Suggest the next one in order.

Foundation order (recommended, not enforced):
1. PRD → product-goal → product-principles → personas → product-journey
2. domain-model → business-rules → data-model
3. ux-spec → ui-spec

Show user: "Foundation phase. Missing: [list]. Suggested next: [first missing]."

---

### ARCHITECTURE phase
**Condition:** Foundation docs exist AND any of these missing:
- `docs/04_tech/backend_architecture.md`
- `docs/04_tech/frontend_architecture.md`
- `docs/05_scrum/definition_of_ready.md`
- `docs/05_scrum/definition_of_done.md`

**Action:** Show which architecture/agreement docs are missing.

Architecture order (recommended):
1. backend-architecture
2. frontend-architecture
3. definition-of-ready + definition-of-done (can run in parallel)
4. risk-docs

Show user: "Architecture phase. Missing: [list]. Suggested next: [first missing]."

---

### SLICE CYCLE phase
**Condition:** Foundation + Architecture docs exist.

Within the slice cycle, determine sub-state:

**A — No active slice:**
> "Ready to start slice discovery. No active slice in memory."  
Suggest: `kick-development:slices-discovery`

**B — Discovery done for S#, no backlog yet:**
> "S[N] discovery complete. Next: create backlog for S[N]."  
Suggest: `kick-development:backlog`

**C — Backlog exists, no sprint planned:**
> "Backlog ready. Next: plan Sprint [N] from S[N] stories."  
Suggest: `kick-development:sprint-planning`

**D — Sprint active (Planning done, Review not done):**
> "Sprint [N] in progress. [X] stories active. Blocking issues: [from memory]."  
Show sprint state. Ask if any stories are done or if there are blockers to record.  
When sprint is complete: suggest `kick-development:sprint-review`

**E — Sprint review done:**
> "Sprint [N] closed. S[N] [complete/partial]."  
If slice complete: suggest next slice discovery.  
If slice incomplete: suggest continue with remaining stories or reprioritize.

---

## Step 3 — Show state and ask

Present to user:

```
Project: [name from PRD or memory]
Phase: [Foundation / Architecture / Slice Cycle]
Active slice: [S# or None]
Sprint: [Sprint N — state | None]
Blockers: [list or None]

Suggested next: [concrete action]
```

Use AskUserQuestion:
- Option A: "[Suggested next action]" (Recommended)
- Option B: "Show full doc status"
- Option C: "Do something different"

If user picks C, show full phase table and let them pick.

---

## Step 4 — Invoke skill

Call the skill for the chosen action. Pass relevant context if the skill needs it.

After the skill completes, **always update `project_memory.md`**.

---

## Memory Format

File: `project_memory.md` in project root.

```markdown
# Project Memory

**Last updated:** [date]
**Project:** [name]

## Phase
[Foundation | Architecture | Slice Cycle]

## Active Slice
[S# — name | None]

## Sprint
[Sprint N — Planning | In Progress | Review | Closed | None]

## Completed
- [Foundation docs: done/partial]
- [Architecture docs: done/partial]
- [S1: Discovery ✅ | Backlog ✅ | Sprint 1 ✅ | Sprint 2 ✅]
- [S2: Discovery ✅ | Backlog ⬜ | ...]

## Blockers
- [blocker — what it blocks]

## Open Decisions
- [decision pending — context]

## Last Action
[What was done last session]
```

Update memory after EVERY guide session. Specifically update:
- Phase if it changed
- Active slice if discovery was completed
- Sprint state if planning/review happened
- Completed list
- Blockers (add or remove)
- Last Action

---

## Full Doc Status Table (show when user requests)

| Phase | Document | Status | Skill |
|-------|----------|--------|-------|
| **Product** | PRD | ⬜/✅ | `kick-development:prd` |
| **Product** | Product Goal | ⬜/✅ | `kick-development:product-goal` |
| **Product** | Product Principles | ⬜/✅ | `kick-development:product-principles` |
| **Product** | Personas | ⬜/✅ | `kick-development:personas` |
| **Product** | Product Journey | ⬜/✅ | `kick-development:product-journey` |
| **Business** | Domain Model | ⬜/✅ | `kick-development:domain-model` |
| **Business** | Business Rules | ⬜/✅ | `kick-development:business-rules` |
| **Business** | Data Model | ⬜/✅ | `kick-development:data-model` |
| **Design** | UX Spec | ⬜/✅ | `kick-development:ux-spec` |
| **Design** | UI Spec | ⬜/✅ | `kick-development:ui-spec` |
| **Tech** | Backend Architecture | ⬜/✅ | `kick-development:backend-architecture` |
| **Tech** | Frontend Architecture | ⬜/✅ | `kick-development:frontend-architecture` |
| **Scrum** | Definition of Ready | ⬜/✅ | `kick-development:definition-of-ready` |
| **Scrum** | Definition of Done | ⬜/✅ | `kick-development:definition-of-done` |
| **Scrum** | Slice Discovery S# | ⬜/✅ | `kick-development:slices-discovery` |
| **Scrum** | Backlog | ⬜/✅ | `kick-development:backlog` |
| **Scrum** | Sprint Plan | ⬜/✅ | `kick-development:sprint-planning` |
| **Scrum** | Sprint Review | ⬜/✅ | `kick-development:sprint-review` |
| **Decisions** | Risk Register | ⬜/✅ | `kick-development:risk-docs` |
| **Decisions** | Decision Log | ⬜/✅ | `kick-development:decision-docs` |

---

## Doc Staleness Rules

If a skill finds a conflict between a canonical doc and reality, guide enforces this:

| Trigger | Update |
|---------|--------|
| New business rule found in discovery | → update `docs/02_business/business_rules.md` |
| Architecture decision changed | → update `docs/04_tech/backend_architecture.md` / `docs/04_tech/frontend_architecture.md` + `docs/06_decisions/` |
| UX flow changed during sprint | → update `docs/03_design/ux_spec.md` |
| Slice complete with learnings | → update `project_memory.md` |

Guide flags staleness but does not auto-update. Always asks user first.

---

## Incremental Development Principles (guide enforces these)

1. **No sprint without DoR met.** If stories aren't Ready, block Sprint Planning.
2. **No slice backlog without discovery.** If S# discovery doesn't exist, block backlog generation.
3. **No Done without DoD met.** Sprint review checks every story against DoD.
4. **Foundation docs update when reality changes.** Discovery that reveals a new business rule → update canon.
5. **One active slice at a time.** Don't start S2 discovery if S1 backlog isn't created.
