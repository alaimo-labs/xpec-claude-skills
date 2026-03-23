---
description: Start implementing a specification. Discovers the spec, reads relevant sections, updates status, and guides you through implementation.
argument-hint: [spec-name-or-id]
---

# Implement a Specification

You are about to implement a specification from Xpec. Follow these steps:

1. **Find the spec:** Use `listSpecifications` to find the spec matching "$ARGUMENTS". If no argument was given, list specs with `purpose: "implement"` and ask the user which one to work on.

2. **Read key sections:** Once you have the spec ID, use `getSpecificationSections` to read `overview`, `user-stories`, and `success-criteria`. These are the minimum you need to start. If any of these sections are not present, pick the closest in meaning.

3. **Confirm understanding:** Summarize what needs to be built in 3-5 bullet points. Ask the user to confirm before proceeding.

4. **Update status:** Set the spec to `IN_PROGRESS` using `updateSpecStatus` if it wasn't already `IN_PROGRESS`.

5. **Read additional sections as needed:** If implementation requires UI work, fetch `wireframes`. If data modeling is involved, fetch `data-model`. Read progressively.

6. **Implement:** Write the code. Follow the acceptance criteria closely.

7. **Record decisions:** As you make implementation choices, use `addSpecNotes` to append notes about decisions, deviations, or open questions.

8. **Record Progress:** When the implementation (or partial implementation) is finished, update the status with a summary of what was done, what's complete and what's pending using `addSpecNotes`

9. **Wrap up:** When done, ask the user if the spec should be marked as `COMPLETED`.
