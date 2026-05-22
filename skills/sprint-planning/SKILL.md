---
name: sprint-planning
description: Use when planning a sprint. Reads the backlog for the active slice, checks stories against Definition of Ready, defines Sprint Goal, and writes the sprint plan. Requires backlog and DoR to exist.
---

# Sprint Planning

Select stories from the active slice backlog, verify they meet DoR, define Sprint Goal, and write the sprint plan.

**Requires:**
- `05_scrum/backlog.md` with at least one slice section
- `05_scrum/definition_of_ready.md`
- Active slice in `project_memory.md` (or user confirms which slice)

## Process

```
Read memory → Read DoR → Read backlog → DoR check per story
→ Sprint Goal → Capacity → Select stories → Write sprint plan → Update memory
```

---

## Step 0 — Read context

Read in this order:

1. `project_memory.md` → get active slice (S#), last sprint number
2. `05_scrum/definition_of_ready.md` → extract all DoR criteria
3. `05_scrum/backlog.md` → extract stories for the active slice
4. `01_product/02_product_goal.md` if exists → Sprint Goal should advance Product Goal

**If no backlog:** Stop. Tell user to run `kick-development:backlog` first.  
**If no DoR:** Stop. Tell user to run `kick-development:definition-of-ready` first.

Calculate next sprint number: if memory says last sprint was N, this is N+1. If no sprint history, this is Sprint 1.

---

## Step 1 — DoR check

For each story in the active slice backlog, check against every DoR criterion.

Present a table:

| Story | DoR status | Blocking criteria |
|-------|-----------|------------------|
| [story title] | ✅ Ready / ⚠️ Partial / ❌ Not ready | [which criteria fail] |

**Q1:** "Which stories have issues? Do you want to mark any as Not Ready and exclude them, or fix them now?" (free text)

Stories marked Not Ready stay in the backlog as Candidate. They do NOT enter the sprint.

If ALL stories fail DoR: stop. Tell user no sprint can start until at least one story is Ready. Suggest fixing the highest-priority story first.

---

## Step 2 — Sprint Goal

**Q2:** "What is the Sprint Goal? Complete: 'By end of this sprint, [user/team] can [observable outcome].'" (free text)

The Sprint Goal must:
- Be achievable with the Ready stories available
- Connect to an outcome from Product Goal or active slice
- Be a single sentence

If the user struggles, suggest one based on the slice scope and ready stories.

---

## Step 3 — Capacity

**Q3:** "How many story points can the team deliver this sprint?" (free text)
Example: "15 points", "not sure — use all Ready stories"

If "not sure": include all Ready stories. Note in the plan that capacity is unestimated.

**Q4:** "Are there any risks or dependencies for this sprint that aren't in the backlog?" (free text or "None")

---

## Step 4 — Story selection

From Ready stories, select those that fit capacity and align with Sprint Goal.

Present selected stories to user:

> "Proposed sprint backlog: [list stories with points, total = X/Y capacity]"

**Q5:** "Any changes to this selection?" (free text or "Looks good")

---

## Document Generation

File: `05_scrum/sprints/sprint-[N].md`

```markdown
# Sprint [N]

**Project:** [name]
**Slice:** S[#]
**Start date:** [today]
**End date:** [today + sprint length from DoD or default 2 weeks]
**Status:** Planning

## Sprint Goal

[Q2]

## Sprint Backlog

| Story | Points | Status | Slice |
|-------|--------|--------|-------|
| [story title] | [N] | To Do | S[#] |
| [...] | | | |

**Total capacity:** [selected] / [available] SP

## Stories Excluded (Not Ready)

| Story | Reason |
|-------|--------|
| [story] | [which DoR criteria failed] |

## Risks This Sprint

[Q4 — or "None identified"]

## Links

- Slice discovery: `05_scrum/discovery/S[#].md`
- Backlog: `05_scrum/backlog.md`
- DoR: `05_scrum/definition_of_ready.md`
- DoD: `05_scrum/definition_of_done.md`
```

---

## File Output

- Create `05_scrum/sprints/` if missing
- Write to `05_scrum/sprints/sprint-[N].md`
- Update `project_memory.md`: set Sprint to "Sprint N — In Progress", update Active Slice, update Last Action

---

## Quality Check Before Writing

- Sprint Goal is a single sentence with observable outcome
- Every included story passed DoR
- Total SP within capacity (or capacity flagged as unestimated)
- Excluded stories have explicit reason
