---
description: Review a specification for completeness and clarity before implementation begins.
argument-hint: [spec-name-or-id]
---

# Review a Specification

You are reviewing a specification from Xpec for quality and completeness. Follow these steps:

1. **Find the spec:** Use `listSpecifications` with `purpose: "review"` to find the spec matching "$ARGUMENTS". If no argument was given, list specs with `purpose: "review"` and ask the user which spec to review.

2. **Read all sections:** Use `getFullSpecification` with `includeContext: true` to get the complete picture. A review requires the full content.

3. **Evaluate the spec** against these criteria:
   - **Clarity:** Are requirements unambiguous? Could a developer implement this without guessing?
   - **Completeness:** Are user stories covered? Are acceptance criteria specific and testable?
   - **Consistency:** Do sections contradict each other?
   - **Feasibility:** Are there obvious technical blockers or missing technical context?

4. **Present findings** as a structured review:
   - What's good and ready
   - What needs clarification (with specific questions)
   - What's missing
   - Suggested improvements

5. **Submit the review:** Use `addSpecReview` to submit your review findings as markdown. This saves the review to the spec for the team.
