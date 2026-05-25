---
name: backlog
description: Use when creating backlog items (PBIs) for a software project. Requires slice discovery documents to exist. Generates verifiable user stories per slice and writes to 05_scrum/.
---

# Backlog

Generate PBIs (Product Backlog Items) from completed slice discovery documents. Each story is traceable to a slice.

**Requires:** At least one `docs/05_scrum/discovery/S#.md` file.  
**Does not generate:** epics invented from thin air, stories without slice traceability, estimates without scope.

## Process

```
Scan slices → Select slices to backlog → Per slice: generate stories
→ User reviews + adjusts → Write
```

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Scan slices (required)

Run:
```bash
find docs/05_scrum/discovery -name "S*.md" | sort
```

Also read:
- `docs/01_product/04_personas.md` → for "As a [persona]" format
- `docs/05_scrum/definition_of_ready.md` → if exists, use its AC format

**If no slice files found:**
> "No slice discovery documents found in docs/05_scrum/discovery/. Backlog requires at least one completed slice. Run pi-dev:slices-discovery first."

Stop and offer to invoke `pi-dev:slices-discovery`.

**If slices found:** List them to the user:
> "Found [N] slice(s): [S1: name], [S2: name], ..."

## Step 1 — Select scope

**Q1:** "Which slices should I generate PBIs for?" (AskUserQuestion)
Options: All slices / Only S[N] / Select specific ones (list them)

If user selects specific ones, ask which by name.

## Step 2 — Per slice: story generation

For each selected slice, read its `S#.md` fully. Extract:
- Scope (inside/outside)
- Business rules affected
- UX flows involved
- Frontend/backend work described
- Decisions and assumptions

Generate 3–7 stories per slice following this logic:
- One story per meaningful user-visible capability within the slice scope
- If scope has multiple distinct user actions → multiple stories
- If scope is thin → fewer stories, don't pad
- Stories stay within the slice's explicit scope — nothing from "outside" section

**Story format:**
```
As a [persona from personas.md or "user"], I want [action], so that [outcome].

Acceptance criteria:
- [ ] [What "done" looks like end-to-end — user visible]
- [ ] [Key business rule enforced — reference rule if applicable]
- [ ] [Failure/edge case handled]

Story points: [1 / 2 / 3 / 5 / 8]
Priority: [Must / Should / Could / Won't]
Slice: [S#]
```

**Story point guide:**
- 1 = trivial, no unknowns, < half a day
- 2 = simple, clear, 1 day
- 3 = moderate, some decisions, 2–3 days
- 5 = complex, multiple moving parts, most of a sprint
- 8 = too big — must be split before sprint

If a story estimates to 8, flag it: "This story may be too large. Consider splitting."

After generating stories for each slice, show them to the user and ask:
**"Are there missing stories, stories to split, or stories to remove for [Slice S#]?"** (free text)

## Step 3 — Prioritization

**Q2:** "How should stories be prioritized across slices?" (AskUserQuestion)
Options: MoSCoW / Slice order (S1 before S2) / Business value first / As generated

## Document Generation

```markdown
# Product Backlog

**Project:** [name]
**Date:** [today]
**Slices covered:** [S1, S2, ...]
**Prioritization:** [Q2]

---

## S[N]: [Slice name]

> Derived from: `docs/05_scrum/discovery/S[N].md`

### Story [N].1: [Short title]

**As a** [persona], **I want** [action], **so that** [outcome].

**Acceptance criteria:**
- [ ] [criterion 1]
- [ ] [criterion 2]
- [ ] [criterion 3]

**Story points:** [estimate]  
**Priority:** [Must/Should/Could/Won't]  
**Slice:** S[N]

---

[Repeat per story]

---

[Repeat section per slice]

## Summary

| Slice | Stories | Total SP | Must stories |
|-------|---------|----------|--------------|
| S[N] | [n] | [total] | [n must] |
| **Total** | | | |
```

## File Output

Write to `docs/05_scrum/backlog.md`. Create folder if missing.  
If file exists, ask: "Overwrite or append new slices?"
