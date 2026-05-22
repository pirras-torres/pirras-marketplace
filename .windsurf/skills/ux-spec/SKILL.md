---
name: ux-spec
description: Use when creating a UX specification. Documents user flows, task analysis, navigation structure, interaction logic, and information architecture. Pure UX only — no visual design, colors, typography, or component details.
---

# UX Specification

Documents the user experience: what users do, how they navigate, what they achieve, and what happens when things go wrong. No visual design here — that lives in `ui-spec`.

**UX covers:** flows, tasks, navigation, IA, interaction logic, error states, empty states, decision points.  
**UX does NOT cover:** colors, typography, spacing, components, layout, visual hierarchy.

## Process

```
Scan context → Platform + constraints → Information architecture
→ Key user flows → Per flow: steps + decision points + failure states
→ Navigation structure → Empty and error states → Write
```

## Step 0 — Scan context

Before asking anything:
- Read `01_product/01_prd.md` → product name, target user, value proposition
- Read `01_product/04_personas.md` → who the user is
- Read `01_product/05_product_journey.md` → journey stages
- Read `02_business/domain_model.md` → entities the user interacts with
- Tell user what you found. Confirm it's current.

## Step 1 — Platform and scope

**Q1:** "What platform is this for?" (AskUserQuestion options: Mobile iOS/Android / Web browser / Desktop / Multiple)

**Q2:** "Are there experience constraints I should know about?" (free text)
Examples: "must work offline", "users are not tech-savvy", "accessibility required (WCAG AA)", "one-handed use on mobile"

## Step 2 — Information architecture

**Q3:** "What are the main sections or areas of the product? (top-level navigation)" (free text)
Example: "Dashboard, Accounts, Transactions, Settings"

**Q4:** "How do users move between sections? Describe the navigation model." (free text)
Example: "Bottom tab bar", "Side drawer", "Top nav with nested pages", "Single-page with modals"

For each section the user lists, ask:
**"What does [section] contain? What can the user do there?"** (free text)

## Step 3 — Key user flows

**Q5:** "What are the 3-5 most critical tasks a user must complete in this product?" (free text)
Example: "Add an account", "Record a transaction", "Check available balance", "Make a credit payment"

For each task, walk through it completely:

**Q6a:** "What triggers [task]? Where does the user start?" (free text)

**Q6b:** "Walk through the steps: what does the user do at each step?" (free text)
Push for specifics: "User taps X → sees Y → selects Z → confirms → arrives at W"

**Q6c:** "What decisions does the user make during this flow? (branching points)" (free text)
Example: "User chooses account type → flow branches to cash / debit / credit path"

**Q6d:** "What can go wrong? List failure states and what the user experiences." (free text)
Example: "Insufficient balance → system blocks action + shows message", "No accounts yet → empty state with CTA"

## Step 4 — Empty states and edge cases

**Q7:** "For each main section, what does the user see when there is no data yet?" (free text)
Empty states are UX decisions — define them explicitly, not as "TBD".

**Q8:** "Are there states that require user action before continuing? (onboarding gates, required setup)" (free text)

## Step 5 — Interaction logic

**Q9:** "Are there any non-obvious interaction rules? (things a developer would not guess)" (free text)
Examples: "Deleting an account requires confirming coverage of linked transactions first", "Payments can only be made from debit/cash accounts, never from credit"

**Q10:** "What confirmations does the user need to see before irreversible actions?" (free text)

## Document Generation

```markdown
# UX Specification

**Project:** [name]
**Platform:** [Q1]
**Status:** Foundational UX spec
**Date:** [today]

> This document covers user experience only: flows, tasks, navigation, and interaction logic.
> Visual design (colors, typography, components, spacing) is documented in `03_design/ui_spec.md`.

## 1. Context

[Product name and core value from PRD. Target user from personas.]

**Experience constraints:** [Q2]

## 2. Information Architecture

**Navigation model:** [Q4]

### Sections

| Section | Purpose | Key tasks |
|---------|---------|-----------|
| [section 1] | [Q3 purpose] | [Q3 tasks] |
| [...] | [...] | [...] |

## 3. User Flows

### Flow: [Task name]

**Trigger:** [Q6a — where user starts]

**Steps:**
1. User: [action] → System: [response/state change]
2. User: [action] → System: [response]
3. [...]

**Decision points:**
- If [condition A] → [path A]
- If [condition B] → [path B]

**Failure states:**
- [Failure 1]: [what user experiences]
- [Failure 2]: [what user experiences]

**End state:** [what success looks like for the user]

---

[Repeat for each flow]

## 4. Empty States

| Section | Empty state | User action available |
|---------|------------|----------------------|
| [section] | [Q7 description] | [CTA or none] |

## 5. Onboarding and Gates

[Q8 — required setup or onboarding gates before core flows are available]

## 6. Interaction Rules

[Q9 — non-obvious rules the system enforces]

**Confirmations required before irreversible actions:**
[Q10]
```

## File Output

- Create `03_design/` if missing
- Write to `03_design/ux_spec.md`
- After writing, offer to create `03_design/ui_spec.md` using `kick-development:ui-spec`

## Quality Check Before Writing

- Every flow has at least one failure state
- Every section has an empty state defined
- No mention of colors, fonts, spacing, or component names
- Interaction rules reference domain entities (from domain model), not visual elements
