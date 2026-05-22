# kick-development

Skills for building software projects incrementally with Scrum documentation.

Each skill reads existing project docs for context, interviews you on decisions relevant to YOUR project, and writes `.md` files. All skills are autonomous — run any one independently, or use the `guide` skill to navigate.

## Skills (19)

| Skill | Output | Phase |
|-------|--------|-------|
| `guide` | — | Navigator |
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
| `slices-discovery` | `05_scrum/discovery/S#.md` | Scrum |
| `backlog` | `05_scrum/backlog.md` | Scrum |
| `definition-of-ready` | `05_scrum/definition_of_ready.md` | Scrum |
| `definition-of-done` | `05_scrum/definition_of_done.md` | Scrum |
| `risk-docs` | `06_decisions/risk_docs.md` | Decisions |
| `decision-docs` | `06_decisions/adr-N-slug.md` | Decisions |

## Recommended Order for New Projects

1. Product phase (start with `prd`)
2. Business phase
3. Design phase
4. Tech phase
5. Scrum phase (`slices-discovery` before `backlog`)
6. Decisions phase

## Key Dependencies

- `backlog` requires at least one `05_scrum/discovery/S#.md` (run `slices-discovery` first)
- `backend-architecture` and `frontend-architecture` adapt to whatever docs already exist
- All other skills are autonomous

## Install

```bash
/plugin install kick-development@<your-marketplace>
```

Or clone locally and register as a local plugin.

## How It Works

Each skill:
1. Scans existing project docs for context
2. Determines what decisions/questions are relevant to THIS project
3. Interviews you using AskUserQuestion
4. Generates the document
5. Writes the `.md` file to the appropriate folder
