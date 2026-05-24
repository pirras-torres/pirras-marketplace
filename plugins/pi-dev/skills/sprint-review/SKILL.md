---
name: sprint-review
description: Use when closing a sprint. Checks stories against Definition of Done, records what was completed, identifies canonical docs that need updating, captures retrospective insights, and prepares the next slice or sprint.
---

# Sprint Review

Close a sprint, verify Done criteria, identify doc updates needed, capture learnings, and determine next step.

**Requires:**
- `docs/05_scrum/sprints/sprint-[N].md` (the active sprint plan)
- `docs/05_scrum/definition_of_done.md`

## Process

```
Read sprint + DoD → Per story: Done check → Identify doc updates
→ Retrospective → Next step decision → Update sprint + memory
```

---

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Read context

1. `project_memory.md` → current sprint N, active slice S#
2. `docs/05_scrum/sprints/sprint-[N].md` → sprint backlog and Sprint Goal
3. `docs/05_scrum/definition_of_done.md` → all DoD criteria
4. `docs/05_scrum/discovery/S[#].md` → slice sufficiency criteria (was the slice goal met?)

Tell user: "Reviewing Sprint [N] for slice S[#]. Sprint Goal: [goal]. [X] stories in sprint."

---

## Step 1 — Story DoD check

For each story in the sprint, ask:

**Q1a:** "For '[story title]': does it meet all DoD criteria? What evidence exists?" (free text)

Accepted evidence examples: "tests pass", "deployed to staging", "PO verified", "acceptance criteria checked"

Mark each story:
- ✅ **Done** — all DoD criteria met with evidence
- ⚠️ **Partial** — some criteria met, some not
- ❌ **Not Done** — did not progress or major criteria failed

**Partial and Not Done stories go back to backlog as Candidate.** They are NOT marked Done.

Present summary table after all stories:

| Story | Status | Evidence | Next |
|-------|--------|----------|------|
| [story] | ✅ Done | [evidence] | — |
| [story] | ⚠️ Partial | [what's done] | Back to backlog |
| [story] | ❌ Not Done | — | Back to backlog |

---

## Step 2 — Sprint Goal assessment

**Q2:** "Was the Sprint Goal achieved? Describe what the user can now do that they couldn't before." (free text)

This is the outcome check — not just whether stories are done, but whether real value was delivered.

---

## Step 3 — Canonical doc updates

Based on what was built, check if any docs need updating:

**Q3:** "Did this sprint reveal anything that contradicts or extends existing canonical docs? (new business rule, changed UX flow, architecture decision, new entity)" (free text or "Nothing")

For each item identified:
**Q4:** "Which canonical doc should be updated? I'll invoke the right skill after review." (free text)

**Promotion rule:** anything stable found during a sprint that isn't in canonical docs must be updated before the next discovery. Guide will flag this.

---

## Step 4 — Retrospective (brief)

**Q5:** "What went well this sprint?" (free text — 1-3 items)

**Q6:** "What slowed you down or should change next sprint?" (free text — 1-3 items)

**Q7:** "Any process changes for the next sprint?" (free text or "None")

Keep retrospective short. Not a ceremony — just useful signals for the next sprint.

---

## Step 5 — Next step

Determine what comes next:

**Q8:** "Is slice S[#] complete (all planned stories done or deliberately dropped), or does it continue next sprint?" (AskUserQuestion)
Options:
- Slice complete → start next slice discovery
- Slice continues → plan Sprint [N+1] with remaining stories
- Slice needs revision → update discovery doc first

---

## Document Updates

**Update sprint file** `docs/05_scrum/sprints/sprint-[N].md`:

Add to the end:
```markdown
## Review

**Closed:** [today]
**Sprint Goal achieved:** Yes / Partial / No

**Outcome:** [Q2 — what the user can now do]

### Story Results

| Story | Status | Evidence |
|-------|--------|----------|
| [story] | ✅ Done | [evidence] |
| [story] | ⚠️ Partial | Returned to backlog |

### Canonical Docs Updated
[Q3 — list or "None"]

### Retrospective

**Went well:**
- [Q5]

**Improve:**
- [Q6]

**Process change:**
[Q7 or "None"]
```

**Update `project_memory.md`:**
- Sprint: "Sprint N — Closed"
- Completed: add Sprint N result
- Active Slice: update status (complete / continues)
- Blockers: remove resolved ones, add new ones from Q6
- Last Action: "Sprint N reviewed — [brief outcome]"
- Next Action: [what guide should suggest next session]

---

## Quality Check

- Every story has explicit Done/Partial/Not Done status with evidence
- Partial/Not Done stories explicitly returned to backlog
- Sprint Goal has an outcome statement (not just "stories done")
- Canonical doc updates identified or confirmed as "none needed"
- `project_memory.md` updated before closing
