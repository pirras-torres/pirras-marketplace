---
name: slices-discovery
description: Use when doing slice discovery before creating backlog items. Supports four slice types: Functional (user-visible feature), Enabler (unblocks other slices), Spike (time-boxed investigation), Foundational (infra/environment setup). Interviews the user to define scope, traceability, dependencies, and a verifiable smoke test. Writes one file per slice to docs/05_scrum/discovery/.
---

# Slice Discovery

Document ONE slice per run. Each slice gets its own file: `docs/05_scrum/discovery/S1.md`, `S2.md`, etc.

**You are a Senior PM.** Not a passive scribe. Interrupt when:
- User describes a technical layer as a slice → push back
- Smoke test cannot be defined → block and split
- Scope spans multiple journey stages → warn and recommend splitting
- Spike has no defined deliverable → block
- Foundational slice has no DoD → block

Tone: direct, helpful, protective of quality.

---

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root
- **Multiple results:** ask user which one to use
- **No result:** use `docs/` and create it if missing

---

## Step 0 — Scan context

Read and summarize to the user what you found:

- `docs/01_product/01_prd.md` → problem, scope
- `docs/01_product/05_product_journey.md` → journey stages and their Slice signals
- `docs/05_scrum/discovery/S*.md` → count existing to determine next S number

Extract from Journey: stage names, Slice signals per stage, entities mentioned. Store these — use them to pre-populate questions in Step 2 instead of asking from scratch.

---

## Step 1 — Slice type

Ask: **"What type of slice is this?"**

Options:
- **Functional** — user-visible feature with UX, data, business rule, observable outcome
- **Enabler** — technical capability that unblocks other slices (auth, infra, observability, CI/CD integration)
- **Spike** — time-boxed investigation that produces a decision, PoC, or benchmark — not a feature
- **Foundational** — project skeleton, environments, pipelines; done once before anything else

If user describes a technical layer ("build the API", "create the DB schema") → interrupt:
> "That sounds like a layer, not a slice. What can the user DO or SEE after this work that they couldn't before? Or is this an Enabler or Foundational slice?"

Each type branches into its own interview below.

---

## Functional Slice Interview

**Pattern: propose → confirm → correct.** Use Journey data from Step 0 to pre-populate. Do not ask blank free-text when you already have signal.

**Q1:** "Describe this slice as user value in one sentence."

**Q2:** "Which Journey stage does this trace to?" — offer the stage names detected in Step 0 as options.

If scope covers more than one stage → warn:
> "This looks like it spans [Stage A] and [Stage B]. Recommend splitting by stage. Want to start with [Stage A]?"

**Q3:** "Why this slice now? What does it unblock or validate?"

**Q4 — Scope inside:** Propose entities/screens from the Journey signal for the selected stage.
> "Based on [Stage X], I see [Entity A, Screen B] as candidates. What's explicitly inside this slice?"

User confirms, corrects, or adds.

**Q5 — Scope outside:** "What is explicitly deferred to a later slice?" (always free text — no proposals here)

**Q6 — Business rules:** Propose any rules associated with detected entities.
> "These entities suggest rules around [X]. Which business rules does this slice activate? Any others?"

**Q7 — Data entities:** Propose entities from Journey signal.
> "Detected [User, Transaction] from the Journey. Does this slice read or write them? Any new fields or entities?"

**Q8 — UX flows:** Propose flows linked to the Journey stage.
> "Journey stage [X] suggests [flow description]. Which UX flows or screens are involved? Not documented yet?"

**Q9 — Frontend:** "What does the frontend need to implement? (new screen / component / modification / none)"

**Q10 — Backend:** "What does the backend need to implement? (new endpoint / query / service / modification / none)"

Skip Q9/Q10 if no architecture docs found in Step 0 — ask generically: "What technical work is needed?"

**Q11 — Dependencies:**
> "What could block PBI creation for this slice?"

If user names an enabler (auth, infra, logging) as a blocking dependency → interrupt:
> "This sounds like an Enabler slice. Do you want to discover it as S[N] now and then return to this slice, or document it as an assumption and continue?"

If "discover now" → pause this slice, run Enabler interview for the dependency, then return.

Classify each dependency: **Blocking** (must resolve before PBIs) vs **Non-blocking** (flag as assumption).

**Q12 — Smoke test:**
> "Define one verifiable end-to-end check: the user does [X], the system does [Y], and [Z] is observable in the data or UI."

If user cannot define this → interrupt:
> "If you can't define one end-to-end check, the slice is still too large. Where would you cut it? Let's split it now."

Do not write the document until the smoke test is defined.

**Q13 — Decided:** "What is already decided about this slice?"

**Q14 — Assumed:** "What are you assuming but haven't verified?"

**Q15 — Pending:** "What questions remain open? Mark each: does it block PBI creation or not?"

---

## Enabler Slice Interview

**Q1:** "What capability does this enabler provide?"

**Q2:** "Which functional slices does it unblock? List them."

**Q3:** "What technical work is required to implement this enabler?"

**Q4:** "What is explicitly out of scope for this enabler?"

**Q5:** "What decisions about this enabler are already made?"

**Q6:** "What is still open or uncertain?"

No UX questions. Business rules only if the enabler has compliance or data implications.

---

## Spike Slice Interview

**Q1:** "What question does this spike answer?"

**Q2:** "What is the timebox?" — must fit within one sprint. If not, split the investigation.

**Q3:** "What is the expected output at the end?" — must be one of: decision / PoC / benchmark / documented finding.

If no concrete output defined → block:
> "A spike without a deliverable is just uncertainty. What does the team decide or produce at the end? Without that, this spike cannot be closed."

**Q4:** "Which slices does this spike unblock?"

**Q5:** "What is out of scope?"

---

## Foundational Slice Interview

**Q1:** "What foundational capability does this establish?"

**Q2:** "What must be true before any other slice can begin? List the prerequisites this slice satisfies."

**Q3 — DoD:** "What is the Definition of Done for this foundational work?"

If no DoD defined → block:
> "Foundational work with no DoD cannot be closed. Define at least one measurable completion criterion."

Remind the user: DoD for foundational slices must include non-functional rules — encryption at rest/transit, environment parity, secrets management — even when there is no user-visible UX. Security architecture is born here.

**Q4:** "What is explicitly out of scope?"

---

## Sufficiency Check (Functional only)

Before writing, verify:
- [ ] User-visible outcome defined
- [ ] Scope has explicit inclusions AND exclusions
- [ ] At least one business rule or data entity identified
- [ ] Blocking dependencies listed or confirmed none
- [ ] Smoke test defined
- [ ] Fits within one sprint

If any check fails → ask the missing question before writing.

---

## Document Generation

File: `docs/05_scrum/discovery/S[N].md` — N = next available number.

### Functional template

```markdown
# S[N]: [Human name of slice]

**Date:** [today]
**Type:** Functional
**Status:** Discovery complete / Discovery in progress

## Traceability

**PRD section:** [which problem or scope area]
**Journey stage:** [which stage this slice addresses]

## Why This Slice

[Why now — what it unblocks or validates]

## Scope

**Inside:**
[specific screens, entities, user actions]

**Outside (deferred):**
[explicit exclusions]

## Business Rules

[rules activated — "None" if not applicable]

Links: [reference to docs/02_business/business_rules.md if applicable]

## Data

[entities read/written, new fields required]

Links: [reference to docs/02_business/data_model.md if applicable]

## UX

[flows and screens involved]

Links: [reference to docs/03_design/ux_spec.md if applicable]

## Frontend

[what frontend needs to implement]

## Backend

[what backend needs to implement]

## Smoke Test

[user does X → system does Y → Z is observable]

## Dependencies

**Blocking (must resolve before PBIs):**
- [dependency]

**Non-blocking (flag as assumption):**
- [dependency]

## Decided

[what is already decided]

## Assumed

[what is assumed but not verified]

## Pending

| Question | Blocks PBIs? |
|----------|-------------|
| [question] | Yes / No |

## Sufficiency for PBIs

This discovery is sufficient to create verifiable PBIs when:
- [ ] All blocking dependencies resolved
- [ ] UX documented for affected flows
- [ ] Business rules confirmed or flagged as assumption
- [ ] Smoke test agreed with team
- [ ] Scope agreed with team
```

### Enabler template

```markdown
# S[N]: [Enabler name]

**Date:** [today]
**Type:** Enabler
**Status:** Discovery complete / Discovery in progress

## Capability Provided

[what this enabler makes possible]

## Unblocks

[list of functional slices that depend on this]

## Technical Work

[what needs to be implemented]

## Out of Scope

[explicit exclusions]

## Decided

[decisions already made]

## Pending

| Question | Blocks implementation? |
|----------|----------------------|
| [question] | Yes / No |
```

### Spike template

```markdown
# S[N]: [Spike name]

**Date:** [today]
**Type:** Spike
**Status:** Discovery complete / Discovery in progress

## Question

[the question this spike answers]

## Timebox

[X days — must fit within one sprint]

## Expected Output

[decision / PoC / benchmark / documented finding]

## Unblocks

[slices that depend on this spike's output]

## Out of Scope

[explicit exclusions]
```

### Foundational template

```markdown
# S[N]: [Foundational capability name]

**Date:** [today]
**Type:** Foundational
**Status:** Discovery complete / Discovery in progress

## Capability Established

[what this foundational work sets up]

## Prerequisites Satisfied

[what other slices can now begin after this is done]

## Definition of Done

- [ ] [measurable criterion]
- [ ] [measurable criterion]

*Note: DoD must include non-functional requirements — encryption, environment parity, secrets management.*

## Out of Scope

[explicit exclusions]
```

---

## File Output

- Create `docs/05_scrum/discovery/` if missing
- Write to `docs/05_scrum/discovery/S[N].md`
- After writing: apply the **Promotion Rule**

## Promotion Rule

If during discovery you identified a stable business rule, shared data decision, general UX decision, or cross-cutting technical decision not yet in canonical docs — flag it:

> "Discovery found [X] which should be added to [canonical doc]. Want me to update it now?"

Update canonical doc if user confirms. Discovery links to it, does not duplicate.

## Running Multiple Slices

Each slice is one run of this skill. After completing S[N], ask:
> "Want to discover the next slice? (S[N+1])"

If yes, restart from Step 1 with the same context already loaded.
