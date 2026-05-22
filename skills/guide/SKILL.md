---
name: guide
description: Use when starting or continuing a software project and need to know which documentation to create next, or to navigate between documentation phases.
---

# Software Development Guide

Navigator skill. Scans existing docs, shows phase status, and invokes the right skill.

## How to Run

### Step 1 — Scan existing docs

Run this to check what already exists:

```bash
find . -type f -name "*.md" | grep -E "0[1-9]_" | sort
```

Also check for these standard folders: `01_product/`, `02_business/`, `03_design/`, `04_tech/`, `05_scrum/`, `06_decisions/`.

### Step 2 — Show phase status

Present a status table to the user. Mark each document ✅ (file exists) or ⬜ (missing):

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
| **Design** | Prototype Docs | ⬜/✅ | `kick-development:prototype-docs` |
| **Tech** | Backend Architecture | ⬜/✅ | `kick-development:backend-architecture` |
| **Tech** | Frontend Architecture | ⬜/✅ | `kick-development:frontend-architecture` |
| **Scrum** | Slices Discovery | ⬜/✅ | `kick-development:slices-discovery` |
| **Scrum** | Backlog | ⬜/✅ | `kick-development:backlog` |
| **Scrum** | Definition of Ready | ⬜/✅ | `kick-development:definition-of-ready` |
| **Scrum** | Definition of Done | ⬜/✅ | `kick-development:definition-of-done` |
| **Decisions** | Risk Docs | ⬜/✅ | `kick-development:risk-docs` |
| **Decisions** | Decision Docs | ⬜/✅ | `kick-development:decision-docs` |

### Step 3 — Ask what to work on

Use AskUserQuestion to show phases as options. Only show phases that have at least one missing doc.

Example question: "Which phase do you want to work on?"  
Options: Product / Business / Design / Tech / Scrum / Decisions

If the user picks a phase with multiple missing docs, ask which specific document within that phase.

### Step 4 — Invoke the skill

Call the skill listed in the table for the chosen document.

## Recommended Order for New Projects

Product → Business → Design → Tech → Scrum → Decisions

The PRD should exist before Domain Model. Domain Model should exist before Backlog. This is recommended, not enforced — any skill can run standalone.

## Output Folder Conventions

Skills write files to these folders (create if missing):

```
01_product/
02_business/
03_design/
04_tech/
05_scrum/
06_decisions/
```
