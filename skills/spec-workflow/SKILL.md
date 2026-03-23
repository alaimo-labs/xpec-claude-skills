---
name: spec-workflow
description: How to manage specification status and notes in Xpec. Use when the user is working through a spec, needs to update its status, or wants to record progress and decisions.
---

# Specification Workflow

## Purpose

Guide the agent through the spec lifecycle: tracking progress via status updates and recording decisions or findings via notes.

## Status Flow

Specifications follow this lifecycle:

```
DRAFT → REFINING → READY → IN_PROGRESS → COMPLETED
```

- **DRAFT** — Spec is being written (managed by Xpec, not settable by agents)
- **REFINING** — Spec is being refined based on feedback (managed by Xpec, not settable by agents)
- **READY** — Spec is written and approved, waiting for implementation
- **IN_PROGRESS** — Someone is actively working on it
- **COMPLETED** — Implementation is done

## Tools Available

- `updateSpecStatus` — Change a spec's status (`id`, `status`). Only accepts: READY, IN_PROGRESS, COMPLETED.
- `addSpecNotes` — Add notes to a spec (`id`, `notes`, `append`). Defaults to append mode.
- `addSpecReview` — Submit a review for a spec (`specId`, `agentReview`). The review is markdown content saved as a one-way operation (never returned in responses).

## Instructions

### Status Updates

1. **Set to IN_PROGRESS** when the user starts working on a spec.
2. **Set to COMPLETED** when the user confirms the work is done.
3. **Always confirm with the user** before changing status — don't change it silently.

### Notes

1. **Append notes** (default) to record progress, decisions, or blockers as work progresses.
2. **Replace notes** (`append: false`) only when the user explicitly wants to overwrite existing notes.
3. **Good notes include:**
   - Decisions made during implementation and their rationale
   - Deviations from the spec and why
   - Blockers or open questions
   - Links to PRs or commits related to the spec

### Reviews

1. **Use `addSpecReview`** to submit a structured review of a specification.
2. **The `agentReview` parameter** should be markdown-formatted text covering findings, gaps, and suggestions.
3. **Reviews are one-way** — once submitted, the review content is saved but is not returned in subsequent API responses.

## Key Principle

Keep the spec updated as a living document. Notes create a trail of decisions that help the team understand not just what was built, but why.
