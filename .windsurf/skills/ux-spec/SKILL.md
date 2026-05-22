---
name: ux-spec
description: Use when creating UX specifications for a software project. Defines user flows, screens, interactions, and UI copy. Writes to 03_design/.
---

# UX Specification

Interview the user to define user flows, screens, interactions, and copy. Write results to `03_design/ux_spec.md`.

## Process

```
Scan context → Platform + constraints → Key flows → Screen inventory
→ Screen details (per screen) → Interaction patterns → Copy → Generate doc → Write to disk
```

## Step 0 — Scan context

Before asking anything:
- Read `01_product/01_prd.md` if exists → extract product name, target user, value proposition
- Read `01_product/05_product_journey.md` if exists → extract user journey stages
- Read `02_business/domain_model.md` if exists → extract entities that need UI
- Tell the user what context you found. Confirm it's current.

## Step 1 — Platform and constraints

**Q1:** "What platform(s) is this for?" (use AskUserQuestion with options)
Options: Mobile (iOS/Android) / Web browser / Desktop app / Multiple platforms

**Q2:** "Are there any visual or interaction constraints I should know about?" (free text)
Examples: "must work offline", "users are not tech savvy", "dark mode required", "accessible for color blindness"

## Step 2 — Key user flows

**Q3:** "What are the 3-5 most important things a user needs to do in this product? List them as actions." (free text)
Example: "Add a bank account", "View current available balance", "Record a purchase", "Cover a credit card payment"

For each flow the user lists, ask:
**"Walk me through [flow name] step by step. What does the user do, what does the system do, what does the user see?"** (free text)

If the user gives a vague answer, prompt: "What triggers this flow? What is the happy path? What can go wrong?"

## Step 3 — Screen inventory

Based on the flows described, propose a screen list. Tell the user:
"Based on what you described, I think these are the main screens: [list]. Does this look right? What's missing?"

**Q4 (confirmation):** "Here is the proposed screen list: [list]. Any screens to add, remove, or rename?" (free text)

## Step 4 — Screen details (repeat per screen)

For each screen in the inventory, ask:

**Q5a:** "What is the purpose of [Screen Name]? What question does this screen answer for the user?" (free text)

**Q5b:** "What are the key elements on this screen? (list the most important data shown and actions available)" (free text)

**Q5c:** "What is the primary action on this screen?" (free text — one action per screen)

**Q5d:** "What edge cases or empty states does this screen need to handle?" (free text)

Do NOT ask all 4 sub-questions at once. Ask Q5a, get answer, then Q5b, etc.

## Step 5 — Interaction patterns

**Q6:** "Are there any recurring interaction patterns? (gestures, transitions, confirmations, toasts, etc.)" (free text)
Example: "Swipe left to delete", "Tap to expand detail", "Confirm before destructive actions"

**Q7:** "How does the product handle errors? What does the user see when something goes wrong?" (free text)

## Step 6 — UI Copy style

**Q8:** "What is the tone of voice for this product? Pick the closest." (AskUserQuestion with options)
Options: Conversational and warm / Clear and direct / Professional and formal / Playful and casual

**Q9:** "Are there any copy examples you already have? Paste them, or describe the style." (free text — optional)

## Document Generation

Generate `03_design/ux_spec.md`:

```markdown
# UX Specification

**Project:** [name]
**Platform:** [Q1]
**Status:** Foundational UX spec
**Date:** [today]

## 1. Context

[Product name and core value from PRD]

**Target user:** [from PRD]

**Platform constraints:** [Q2]

## 2. Key User Flows

### Flow: [Flow 1 name]

**Trigger:** [what starts this flow]

**Steps:**
1. [User action]
2. [System response]
3. [...]

**Happy path outcome:** [what success looks like]

**Failure states:** [what can go wrong]

---

[Repeat for each flow]

## 3. Screen Inventory

| Screen | Purpose | Key action |
|--------|---------|------------|
| [Screen 1] | [Q5a] | [Q5c] |
| [...] | [...] | [...] |

## 4. Screen Details

### [Screen 1]

**Purpose:** [Q5a]

**Key elements:**
- [Data/element 1]
- [Data/element 2]
- [...]

**Primary action:** [Q5c]

**Edge cases:**
- Empty state: [description]
- [Other edge case]

---

[Repeat for each screen]

## 5. Interaction Patterns

[Q6 — recurring patterns]

**Error handling:** [Q7]

## 6. Copy Style

**Tone:** [Q8]

**Style notes:** [Q9 if provided]

**Key copy principles:**
- [Derived from tone and style]
```

## File Output

- Create `03_design/` folder if missing
- Write to `03_design/ux_spec.md`
- After writing, offer to create `03_design/prototype_docs.md` with annotated screen descriptions using `kick-development:prototype-docs`

## Quality Check Before Writing

- Every screen has a defined primary action
- Every key flow has at least one failure state defined
- Empty states are specified for screens that can have no data
- Copy tone is consistent and can be tested against a real sentence
