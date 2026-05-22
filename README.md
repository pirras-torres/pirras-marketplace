# kick-development

Skills for building software projects incrementally with Scrum documentation.

Each skill interviews you section by section and writes a `.md` file to your project. All skills are autonomous — run any one independently, or use the `guide` skill to navigate.

## Skills

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
| `prototype-docs` | `03_design/prototype_docs.md` | Design |
| `backend-architecture` | `04_tech/backend_architecture.md` | Tech |
| `frontend-architecture` | `04_tech/frontend_architecture.md` | Tech |
| `slices-discovery` | `04_tech/slices_discovery.md` | Tech |
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
5. Scrum phase
6. Decisions phase

## Install

```bash
/plugin install kick-development@<your-marketplace>
```

Or clone locally and register as a local plugin.

## How It Works

Each skill:
1. Scans existing docs in your project for context
2. Interviews you section by section using AskUserQuestion
3. Generates the document
4. Writes the `.md` file to the appropriate folder
