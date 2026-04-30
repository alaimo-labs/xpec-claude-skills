---
description: Start implementing a specification. Discovers the spec, reads relevant sections, updates status, and guides you through implementation.
argument-hint: [spec-name-or-id]
---

# Implement a Specification

You are about to implement a specification from Xpec. Follow these steps:

1. **Find the spec:** Use `listSpecifications` to find the spec matching "$ARGUMENTS". If no argument was given, list specs with `purpose: "implement"` and ask the user which one to work on.

2. **Recover progress:** Look at `recordedIterations` from `listSpecifications` (or call `getFullSpecification` if you have the ID directly). If `recordedIterations > 0`, call `getSpecProgress` BEFORE reading sections — the latest iteration's `nextSteps` is your resume point, and the full iterations array (including each iteration's "Open items" subsection) rebuilds the prior context. If `recordedIterations === 0`, you're starting fresh — skip `getSpecProgress`. This applies regardless of the spec's status (READY, IN_PROGRESS, or COMPLETED).

3. **Read key sections:** Use `getSpecificationSections` to read `overview`, `user-stories`, `success-criteria`, AND `exposure-plan` if it appears in the spec's section metadata (it provides the level structure and beliefs the current iteration is testing). If any of these sections are not present, pick the closest in meaning.

4. **Confirm understanding:** Summarize what needs to be built in 3-5 bullet points. Ask the user to confirm before proceeding.

5. **Update status:** Set the spec to `IN_PROGRESS` using `updateSpecStatus` if it wasn't already.

6. **Read additional sections as needed:** If implementation requires UI work, fetch `wireframes`. If data modeling is involved, fetch `data-model`. Read progressively.

7. **Implement:** Write the code. Follow the acceptance criteria closely.

8. **Record iteration:** When closing this iteration — at a natural stopping point or at completion — call `recordSpecProgress` with:
   - **title:** short headline of what this iteration achieved.
   - **details:** rich markdown narrative. Recommended subsections (guide, not enforcement): State, Decisions, Delivered scope, Tests, Out of scope, Open items.
     - **Open items** is for cross-cutting items still being tracked. One bullet per item, prefixed with state (`pending` / `RESOLVED` / `unchanged` / `NEW` / `observation`), brief context, and resolution trigger if applicable. Read the previous iteration's "Open items" and update each entry's state.
   - **nextSteps:** where the next iteration resumes from (or "validation only" if done).

9. **Wrap up:** Ask the user if the spec should be marked as `COMPLETED`.
