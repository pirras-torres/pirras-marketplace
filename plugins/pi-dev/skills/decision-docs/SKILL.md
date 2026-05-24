---
name: decision-docs
description: Use when documenting an architectural or product decision. Creates an Architecture Decision Record (ADR) capturing context, options, and rationale. Writes to docs/06_decisions/.
---

# Decision Documentation (ADR)

Interview the user to document one decision using Architecture Decision Record format. Write to `docs/06_decisions/`.

## What Is an ADR

An ADR captures: the context (why a decision was needed), the options considered, the decision made, and why. Written once, referenced forever. Prevents re-litigating the same decision.

## Process

```
One decision per ADR → Context → Options → Decision → Consequences → Write
```

## Detect docs folder

Run:
```bash
find . -maxdepth 3 -type d -name "docs" | grep -v node_modules | grep -v ".git" | sort
```

- **1 result:** use that path as docs root (e.g., `./docs`)
- **Multiple results:** use AskUserQuestion — "Found multiple docs folders: [list]. Which one should I use for this project?"
- **No result:** use `docs/` and create it if missing

## Interview (one question at a time with AskUserQuestion)

**Q1:** "What decision needs to be documented? Phrase it as a question." (free text)
Example: "What database should we use?", "Should we use a monolith or microservices?"

**Q2:** "What is the context? Why does this decision need to be made now?" (free text)

**Q3:** "What options were considered? List 2-4." (free text)
For each option, ask: "What are the pros and cons of [option]?" (free text)

**Q4:** "What was the decision?" (free text)

**Q5:** "Why was this option chosen over the others?" (free text)

**Q6:** "What are the consequences? What becomes easier and what becomes harder because of this decision?" (free text)

**Q7:** "Is this decision reversible? If yes, what would trigger revisiting it?" (free text)

## Document Generation

ADR file name: `docs/06_decisions/adr-[number]-[short-slug].md`
Number increments from existing ADRs in folder.

```markdown
# ADR [number]: [Q1 — decision question as title]

**Status:** Accepted
**Date:** [today]

## Context

[Q2]

## Options Considered

### Option 1: [name]
**Pros:** [...]
**Cons:** [...]

### Option 2: [name]
**Pros:** [...]
**Cons:** [...]

[Repeat for each option]

## Decision

**[Q4]**

[Q5 — rationale]

## Consequences

**Easier:** [Q6 — what improves]

**Harder:** [Q6 — what becomes more difficult or constrained]

## Revisit Trigger

[Q7 — condition that would reopen this decision, or "This decision is irreversible"]
```

## File Output

- Check how many ADRs already exist in `docs/06_decisions/` with `find docs/06_decisions -name "adr-*.md" | wc -l`
- Name file `docs/06_decisions/adr-[N+1]-[slug].md`
- Create folder if missing
- After writing, ask if there are more decisions to document

## Multiple Decisions

If the user needs to document multiple decisions, run the full interview for each one sequentially. Each gets its own ADR file.
