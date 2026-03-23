---
name: spec-sections
description: How to read and interpret specification sections from Xpec. Use when the user asks to read, understand, or analyze a specific specification or its sections.
---

# Reading Specification Sections

## Purpose

Guide the agent through reading and interpreting spec content effectively, fetching only the sections relevant to the task at hand.

## Section Slugs

Specifications are divided into sections identified by slugs. Common slugs include:

- `overview` — High-level description of the feature or product
- `user-stories` — User stories, typically without acceptance criteria
- `user-journey` - User journey for the specification
- `business-rules` - Rules that the software/product should follow
- `visual-interaction-notes` - UI expected behaviour
- `empty-state` - Empty State (if applicable)
- `wireframes` — Visual layout references
- `edge-cases-error-states` - Edge Cases & Error States
- `success-criteria` — Detailed acceptance criteria
- `success-metrics` - Outcome metrics that would measure the feature/spec success in terms of user behaviour or business impact

The actual available slugs vary per spec. Always check what's available via `listSpecifications` before requesting sections.

## Instructions

1. **Match sections to the task:**
   - Implementing a feature? Start with `overview` + `user-stories` + `success-criteria`
   - Designing UI? Start with `wireframes` + `overview` + `visual-interaction-notes` + `empty-state`

2. **Use `getSpecificationSections`** with the spec ID and an array of relevant slugs.

3. **Request more sections only if needed.** If the first sections raise questions, fetch additional ones — don't load everything upfront.

4. **Cross-reference sections** when they relate to each other (e.g., user stories reference acceptance criteria).

## Key Principle

Read sections progressively based on the task. The goal is to understand just enough to act, then go deeper as needed.
