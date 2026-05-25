---
name: ux-spec
description: "Use when creating a UX specification. Documents the user experience screen by screen: what users see, what they can do, what each action triggers, and what happens in edge cases. Pure UX only - no visual design, colors, typography, or component details."
---

# UX Specification

Documents the user experience screen by screen. Each screen gets its own section: content, actions, states, and navigation triggers. Flows are captured as cross-screen sequences.

**UX covers:** what the user sees (content, not visuals), available actions, navigation triggers, decision points, empty/loading/error states, interaction rules.  
**UX does NOT cover:** colors, typography, spacing, component names, layout, visual hierarchy.

## Process

```
Scan context → Confirm screens list → Interview each screen one by one
→ Capture cross-screen flows → Write
```

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use?"
- **No result:** use `docs/` and create it if missing

## Step 0 — Scan context

Before asking anything:
- Read `docs/01_product/01_prd.md` → product name, target user, value proposition
- Read `docs/01_product/04_personas.md` → who the user is
- Read `docs/01_product/05_product_journey.md` → journey stages
- Read `docs/02_business/domain_model.md` → entities the user interacts with
- Tell user what you found. Confirm it's current.

## Step 1 — Platform and constraints

**Q1:** "What platform is this for?" (AskUserQuestion: Mobile iOS/Android / Web browser / Desktop / Multiple)

**Q2:** "Any experience constraints?" (free text)  
Examples: "must work offline", "users are not tech-savvy", "accessibility WCAG AA", "one-handed mobile use"

## Step 2 — Screen inventory

**Q3:** "List all screens (or major views) in the product. Give each a short name."  
Example: "Dashboard, Account Detail, Add Account, Transactions, Settings"

Present the list back. Ask user to confirm or adjust before continuing.

Also ask: **Q4:** "How do users navigate between screens? Describe the navigation model."  
Example: "Bottom tab bar", "Side drawer", "Stack navigation with back", "Single page with modals"

## Step 3 — Screen-by-screen interview

For **each screen** in the confirmed list, run this interview in order. Do one screen at a time — do not batch.

---

**"Let's describe [Screen Name]."**

**Sa:** "What does the user see when they arrive at this screen? Describe the content — not the layout, not the visuals. What information is present?"  
(free text — push for specifics: amounts, labels, lists, counts, summaries)

**Sb:** "What actions can the user take from this screen? List them all — buttons, taps, swipes, links, anything interactive."  
(free text — capture every entry point)

For each action listed in Sb:
**Sc:** "When the user does [action], what happens? Does it open a modal, navigate to another screen, trigger a system change, or something else?"  
(free text — identify the destination or effect of every action)

**Sd:** "What states does this screen have?"  
Prompt for each:
- **Empty state:** what does the user see when there is no data yet?
- **Loading state:** is there a waiting moment? What is the user doing during it?
- **Error state:** what can go wrong here? What does the user experience?
- **Partial state:** are there combinations of data that produce a different view? (e.g., has accounts but no transactions)

**Se:** "Are there non-obvious rules on this screen that a developer would not guess?"  
Examples: "Credit accounts are excluded from the net worth total", "Cash is shown separately because it doesn't count toward available balance"

---

After finishing all screens, ask:

**Q5:** "Are there any cross-screen flows I should document explicitly? (sequences that span multiple screens and have their own logic)"  
Example: "Onboarding setup", "Make a payment end-to-end", "Resolve an overdue debt"

For each cross-screen flow:
- **Trigger:** where does it start and why?
- **Steps:** screen → action → screen → action → ... → end state
- **Decision points:** where does the path branch?
- **Failure states:** what stops the flow and what does the user see?

## Document Generation

```markdown
# UX Specification

**Project:** [name]
**Platform:** [Q1]
**Navigation model:** [Q4]
**Status:** Draft
**Date:** [today]

> UX only: content, actions, states, navigation, interaction rules.
> Visual design lives in `docs/03_design/ui_spec.md`.

## Context

[Product name and core value from PRD. Target user from personas.]

**Experience constraints:** [Q2]

---

## Screens

---

### [Screen Name]

**What the user sees:**  
[Sa — content present on arrival, described as information not visuals]

**Actions available:**

| Action | Triggers |
|--------|---------|
| [action] | [Sc — destination or effect] |
| [...] | [...] |

**States:**

- **Empty:** [Sd empty]
- **Loading:** [Sd loading — omit if not applicable]
- **Error:** [Sd error]
- **Partial:** [Sd partial — omit if not applicable]

**Interaction rules:**  
[Se — non-obvious constraints. Omit section if none.]

```

Each screen generates its own file. Cross-screen flows go in a separate file.

## File Output

- Create `docs/03_design/` if missing
- One file per screen: `docs/03_design/ux_[screen-name-kebab].md`
  - Example: `ux_dashboard.md`, `ux_account_detail.md`, `ux_add_account.md`
- Cross-screen flows: `docs/03_design/ux_flows.md` — only if Q5 produced flows
- After all files written, offer to create UI specs using `pi-dev:ui-spec`

### Screen file template

```markdown
# UX — [Screen Name]

**Project:** [name]  
**Platform:** [Q1]  
**Status:** Draft  
**Date:** [today]

> UX only: content, actions, states, navigation, interaction rules.
> Visual design lives in the corresponding `ui_` file.

## What the user sees

[Sa — content present on arrival, described as information not visuals]

## Actions

| Action | Triggers |
|--------|---------|
| [action] | [destination or effect] |

## States

- **Empty:** [Sd empty]
- **Loading:** [Sd loading — omit if not applicable]
- **Error:** [Sd error]
- **Partial:** [Sd partial — omit if not applicable]

## Interaction rules

[Se — non-obvious constraints. Omit section if none.]
```

### Flows file template (`ux_flows.md`)

```markdown
# UX — Cross-screen Flows

**Project:** [name]  
**Date:** [today]

## Flow: [Flow name]

**Trigger:** [where and why it starts]

**Steps:**
1. [Screen] — User: [action] → [Screen or modal]
2. [Screen] — User: [action] → [outcome]

**Decision points:**
- If [condition] → [path A]
- If [condition] → [path B]

**Failure states:**
- [Failure]: [what user experiences]

**End state:** [what success looks like]

---

[Repeat for each flow]
```

## Quality Check Before Writing

- Every screen has at least one action documented
- Every screen has an empty state defined (even if "not applicable — data always exists")
- Every action has a documented destination or effect
- No mention of colors, fonts, spacing, or component names
- Interaction rules reference domain entities (from domain model), not visual elements
- Cross-screen flows have at least one failure state each
