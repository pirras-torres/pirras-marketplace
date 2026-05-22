---
name: prototype-docs
description: Use when documenting a prototype or wireframes. Describes screens, annotations, and interaction notes in text form. Writes to 03_design/.
---

# Prototype Docs

Interview the user to document prototype screens and annotate interactions. Write to `03_design/prototype_docs.md`.

## Process

```
Scan context → Prototype type → Per screen: layout, elements, annotations → Interaction notes → Write
```

## Step 0 — Scan context

Read `03_design/ux_spec.md` if exists. Use screen inventory and flows as the starting list.

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What type of prototype exists or will be created?" (options: Lo-fi wireframes / Hi-fi mockups / Clickable prototype / Text description only)

**Q2:** "Is there a link to the prototype? (Figma, etc.)" (free text or "No link")

If no link, document screens from scratch. If link exists, describe what to annotate.

For each screen from the UX spec (or that the user lists):

**Q3a:** "Describe the layout of [Screen Name]. What is at the top, middle, bottom?" (free text)

**Q3b:** "What are the interactive elements? (buttons, inputs, swipe areas, links)" (free text)

**Q3c:** "What annotations or notes are important for the developer implementing this?" (free text)
Example: "This button is disabled until both fields are filled", "Scroll is horizontal, not vertical"

**Q4:** "What transitions or animations exist between screens?" (free text or "None")

## Document Generation

```markdown
# Prototype Documentation

**Project:** [name]
**Prototype type:** [Q1]
**Prototype link:** [Q2]
**Date:** [today]

---

## Screen: [Screen Name]

**Purpose:** [from UX spec]

**Layout:**
- Top: [Q3a — what's at top]
- Middle: [what's in main content area]
- Bottom: [nav, CTA, etc.]

**Interactive elements:**
- [element 1]: [behavior]
- [element 2]: [behavior]

**Developer annotations:**
- [Q3c annotation 1]
- [Q3c annotation 2]

---

[Repeat per screen]

## Transitions

[Q4 — transitions between screens]

## Design Decisions to Validate

[Any design decisions that need user testing or product confirmation before implementing]
```

## File Output

Write to `03_design/prototype_docs.md`. Create folder if missing.
