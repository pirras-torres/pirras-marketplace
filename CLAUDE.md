# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

Local marketplace + plugin workspace for **pi-dev** — Claude Code plugin with 21 skills for incremental software development using Scrum documentation.

- `plugins/pi-dev/` — plugin source (skills, manifest, package.json)
- `.agents/plugins/marketplace.json` — local marketplace manifest
- Skills: `plugins/pi-dev/skills/<skill-name>/SKILL.md`


Body is skill prompt — pure markdown, no runtime code.

## 21 Skills and Output Docs

| Skill | Output path (under `docs/`) |
|-------|-----------------------------|
| `guide` | `project_memory.md` (project root) |
| `prd` | `01_product/01_prd.md` |
| `product-goal` | `01_product/02_product_goal.md` |
| `product-principles` | `01_product/03_product_principles.md` |
| `personas` | `01_product/04_personas.md` |
| `product-journey` | `01_product/05_product_journey.md` |
| `domain-model` | `02_business/domain_model.md` |
| `business-rules` | `02_business/business_rules.md` |
| `data-model` | `02_business/data_model.md` |
| `ux-spec` | `03_design/ux_spec.md` |
| `ui-spec` | `03_design/ui_spec.md` |
| `backend-architecture` | `04_tech/backend_architecture.md` |
| `frontend-architecture` | `04_tech/frontend_architecture.md` |
| `definition-of-ready` | `05_scrum/definition_of_ready.md` |
| `definition-of-done` | `05_scrum/definition_of_done.md` |
| `slices-discovery` | `05_scrum/discovery/S#.md` |
| `backlog` | `05_scrum/backlog.md` |
| `sprint-planning` | `05_scrum/sprints/sprint-N.md` |
| `sprint-review` | updates sprint file + `project_memory.md` |
| `risk-docs` | `06_decisions/risk_docs.md` |
| `decision-docs` | `06_decisions/adr-N-slug.md` |

## Skill Dev Rules

1. Edit only in `plugins/pi-dev/skills/` — canonical source.
2. Each skill = single `SKILL.md`. No other files per skill.
3. `description:` frontmatter critical — Claude uses it to route invocations. Keep precise, trigger-condition focused.
4. Skills are pure prompt text. No imports, no runtime code.
5. Skills writing docs must detect docs folder first (bash pattern in existing skills — keep it).
6. Skills with doc dependencies must validate prerequisites before proceeding.

## Skill Dependency Order

```
FOUNDATION (once)
  prd → product-goal → product-principles → personas → product-journey
  domain-model → business-rules → data-model
  ux-spec → ui-spec

ARCHITECTURE (once)
  backend-architecture → frontend-architecture
  definition-of-ready + definition-of-done
  risk-docs

SLICE CYCLE (repeats)
  slices-discovery → backlog → sprint-planning → BUILD → sprint-review
```

Hard dependencies (skill must block if unmet):
- `business-rules` + `data-model` require `domain-model`
- `backlog` requires at least one `05_scrum/discovery/S#.md`
- `sprint-planning` requires `backlog` + `definition-of-ready`
- `sprint-review` requires active sprint plan

## Marketplace / Install

Local manifest: `.agents/plugins/marketplace.json`

Install from target project:
```bash
/plugin marketplace add https://raw.githubusercontent.com/pirras-torres/pirras-marketplace/main/marketplace.json
/plugin install pi-dev
```

Bump version: update **both** `package.json` and `.codex-plugin/plugin.json`.

## project_memory.md

`guide` skill reads/writes `project_memory.md` at project root of whichever project uses plugin (not this repo). Tracks phase, active slice, sprint state, blockers, last action. Guide = entry point, run at session start.
