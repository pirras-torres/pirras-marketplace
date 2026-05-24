# kick-development

Skills for building software projects incrementally with Scrum documentation.

**Start every session with:** `kick-development:guide`

The guide reads `project_memory.md`, determines your current phase, and tells you exactly what to do next.

## Skills (21)

| Skill | Output | Phase |
|-------|--------|-------|
| `guide` | `project_memory.md` | Orchestrator |
| `prd` | `01_product/01_prd.md` | Product |
| `product-goal` | `01_product/02_product_goal.md` | Product |
| `product-principles` | `01_product/03_product_principles.md` | Product |
| `personas` | `01_product/04_personas.md` | Product |
| `product-journey` | `01_product/05_product_journey.md` | Product |
| `domain-model` | `02_business/domain_model.md` | Business |
| `business-rules` | `02_business/business_rules.md` | Business |
| `data-model` | `02_business/data_model.md` | Business |
| `ux-spec` | `03_design/ux_spec.md` | Design |
| `ui-spec` | `03_design/ui_spec.md` | Design |
| `backend-architecture` | `04_tech/backend_architecture.md` | Tech |
| `frontend-architecture` | `04_tech/frontend_architecture.md` | Tech |
| `definition-of-ready` | `05_scrum/definition_of_ready.md` | Scrum |
| `definition-of-done` | `05_scrum/definition_of_done.md` | Scrum |
| `slices-discovery` | `05_scrum/discovery/S#.md` | Scrum |
| `backlog` | `05_scrum/backlog.md` | Scrum |
| `sprint-planning` | `05_scrum/sprints/sprint-N.md` | Scrum |
| `sprint-review` | updates `sprints/sprint-N.md` + `project_memory.md` | Scrum |
| `risk-docs` | `06_decisions/risk_docs.md` | Decisions |
| `decision-docs` | `06_decisions/adr-N-slug.md` | Decisions |

## The Incremental Cycle

```
FOUNDATION (once)
  prd → product-goal → product-principles → personas → product-journey
  domain-model → business-rules → data-model
  ux-spec → ui-spec

ARCHITECTURE (once, updated when decisions change)
  backend-architecture → frontend-architecture
  definition-of-ready → definition-of-done
  risk-docs

SLICE CYCLE (repeats)
  slices-discovery → backlog → sprint-planning
  → BUILD → sprint-review
  → next slice or update docs
```

## Key Dependencies

- `business-rules` requires `domain-model`
- `data-model` requires `domain-model`
- `backlog` requires at least one `05_scrum/discovery/S#.md`
- `sprint-planning` requires `backlog` + `definition-of-ready`
- `sprint-review` requires an active sprint plan

## Install

```bash
/plugin marketplace add <public-repo-url>/.agents/plugins/marketplace.json
/plugin install kick-development
```

This repository includes a Codex marketplace at `.agents/plugins/marketplace.json`.
Publish the repository, then share the marketplace file URL so other users can add
the marketplace and install `kick-development`.

The plugin manifest lives at `.codex-plugin/plugin.json` and points to the
root `skills/` directory. Edit skills only in `skills/`; there is no copied
skills directory under `.agents/`.

## How It Works

1. `guide` reads `project_memory.md` and current doc state
2. Determines phase: Foundation / Architecture / Slice Cycle
3. Suggests concrete next action
4. Invokes the right skill
5. Updates `project_memory.md` after each action
