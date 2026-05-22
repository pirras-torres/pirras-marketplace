---
name: slices-discovery
description: Use when doing slice discovery before creating backlog items. Answers what a slice covers, why it matters, what dependencies exist, and whether there is enough information to create verifiable PBIs.
---

# Slice Discovery

Document ONE slice per run. Each slice gets its own file: `05_scrum/discovery/S1.md`, `S2.md`, etc.

**Discovery answers:** what the slice covers, why it matters, what rules/data/UX/tech are affected, what is decided vs assumed vs pending.  
**Discovery does NOT produce:** PBI lists, acceptance criteria for individual stories, estimates, sprint assignments, or final API contracts.

## What Makes a Good Slice

A slice is valid when it:
- Improves an expected outcome from the Product Goal or reduces a risk that blocks it
- Is traceable to a specific part of the PRD, Product Goal, or Product Journey
- Is vertical: user-visible + data + business rule + observable evidence
- Is smaller than the full product vision
- Leaves something deliberately outside (scope control)
- Enables learning before the full backlog is created

**Antipatterns — reject these:**
- Slice per layer: "Build the frontend", "Build the API", "Build the DB schema"
- Slice so broad it covers the whole product
- Slice chosen because code already exists
- Slice with no user-visible outcome

## Slice Size

A slice should be deliverable within one sprint (1–2 weeks) by the team. If it can't be, it must be split before creating PBIs.

## Process

```
Scan context → Select slice → Traceability → Scope → Business rules + data
→ UX + frontend → Backend → Dependencies → Decisions / Assumptions / Pending
→ Sufficiency check → Write → Promotion rule
```

## Step 0 — Scan context

Read the following and tell the user what you found:
- `01_product/01_prd.md` → problem, scope
- `01_product/02_product_goal.md` → expected outcomes
- `01_product/05_product_journey.md` → journey stages (use as map, not sequence)
- `02_business/domain_model.md` → entities and rules
- `05_scrum/backlog.md` → existing slices already discovered (to assign correct S# number)

Count existing `05_scrum/discovery/S*.md` files to determine the next ID.

## Step 1 — Slice selection

**Q1:** "What slice are we discovering? Describe it in one sentence as user value." (free text)

If the user describes a technical layer ("build the API", "create the database"), push back:
> "That sounds like a layer, not a slice. What can the user DO or SEE after this work that they couldn't before?"

**Q2:** "Which part of the PRD or Product Goal does this slice address?" (free text)
Expected: reference to a specific problem, outcome, or journey stage.

**Q3:** "Why this slice now? What does it unblock or validate?" (free text)

## Step 2 — Scope

**Q4:** "What is explicitly inside this slice?" (free text)
Be specific: which screens, which entities, which user actions.

**Q5:** "What is explicitly outside this slice? (deferred to later slices)" (free text)
This is as important as Q4. No scope without explicit exclusions.

## Step 3 — Business rules and data

**Q6:** "Which business rules from the domain model are activated by this slice?" (free text)
Reference rules by name if possible. If no rules apply, answer "None".

**Q7:** "Which data entities are read or written in this slice?" (free text)
Reference `data_model.md` fields if they exist. New fields required? Flag them.

## Step 4 — UX

**Q8:** "Which user flows or screens from the UX spec are involved?" (free text or "Not documented yet")

If not documented: "What does the user experience in this slice? Describe the flow in steps." (free text)

## Step 5 — Frontend and backend impact

**Q9:** "What does the frontend need to implement for this slice?" (free text)
New screen / new component / modification to existing / none.

**Q10:** "What does the backend need to implement?" (free text)
New endpoint / new query / new service / modification / none.

Ask only for the layers that exist in the project. If no architecture docs found in Step 0, skip layer-specific questions and ask generically: "What technical work is needed?"

## Step 6 — Dependencies

**Q11:** "What dependencies could block PBI creation for this slice?" (free text)
Examples: "UX spec for this screen doesn't exist yet", "Domain model missing [entity]", "API contract for [endpoint] not defined"

Distinguish: **blocking** (must resolve before PBIs) vs **non-blocking** (can proceed, flag as assumption).

## Step 7 — Decisions, assumptions, pending

**Q12:** "What is already decided about this slice?" (free text)

**Q13:** "What are you assuming but haven't verified?" (free text)

**Q14:** "What questions remain open? Mark each: does it block PBI creation or not?" (free text)

## Sufficiency check

Before writing, verify:
- Slice has a user-visible outcome
- Scope has explicit inclusions AND exclusions
- At least one business rule or data entity is identified
- Blocking dependencies are listed (or confirmed none exist)
- The slice fits within one sprint

If any check fails, ask the missing question before writing.

## Document Generation

File: `05_scrum/discovery/S[N].md` where N = next available number.

```markdown
# S[N]: [Human name of slice]

**Date:** [today]
**Status:** Discovery complete / Discovery in progress

## Traceability

**PRD section:** [Q2 — which problem or scope area]
**Product Goal outcome:** [Q2 — which expected outcome]
**Product Journey stage:** [which stage this slice addresses]

## Why This Slice

[Q3 — what it unblocks or validates]

## Scope

**Inside:**
[Q4 — specific screens, entities, user actions]

**Outside (deferred):**
[Q5 — explicit exclusions]

## Business Rules

[Q6 — rules activated. "None" if not applicable]

Links: [reference to 02_business/business_rules.md sections if applicable]

## Data

[Q7 — entities read/written, new fields required]

Links: [reference to 02_business/data_model.md if applicable]

## UX

[Q8 — flows and screens involved]

Links: [reference to 03_design/ux_spec.md if applicable]

## Frontend

[Q9 — what frontend needs to implement]

## Backend

[Q10 — what backend needs to implement]

## Dependencies

**Blocking (must resolve before PBIs):**
- [dependency 1]

**Non-blocking (flag as assumption):**
- [dependency 1]

## Decided

[Q12]

## Assumed

[Q13]

## Pending

| Question | Blocks PBIs? |
|----------|-------------|
| [Q14 question 1] | Yes / No |

## Sufficiency for PBIs

This discovery is sufficient to create verifiable PBIs when:
- [ ] All blocking dependencies resolved
- [ ] UX documented for affected flows
- [ ] Business rules confirmed or flagged as assumption
- [ ] Scope agreed with team
```

## File Output

- Create `05_scrum/discovery/` if missing
- Write to `05_scrum/discovery/S[N].md`
- After writing: apply the **Promotion Rule**

## Promotion Rule

If during discovery you identified a stable business rule, shared data decision, general UX decision, or cross-cutting technical decision that is NOT yet in the canonical docs — flag it:

> "Discovery found [X] which should be added to [canonical doc]. Want me to update it now?"

Update canonical doc if user confirms. Discovery links to it, does not duplicate it.

## Running Multiple Slices

Each slice is one run of this skill. After completing S1, ask:
> "Want to discover the next slice? (S[N+1])"

If yes, restart from Step 1 with the same context already loaded.
