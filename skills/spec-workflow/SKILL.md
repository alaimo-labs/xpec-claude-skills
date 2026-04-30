---
name: spec-workflow
description: How to manage specification status and notes in Xpec. Use when the user is working through a spec, needs to update its status, or wants to record progress and decisions.
---

# Specification Workflow

## Purpose

Guide the agent through the spec lifecycle: tracking progress via status updates, recording iteration entries, and authoring exposure plans for planning-time skills.

## Status Flow

Specifications follow this lifecycle:

```
DRAFT → REFINING → READY → IN_PROGRESS → COMPLETED
```

- **DRAFT** — Spec is being written (managed by Xpec, not settable by agents).
- **REFINING** — Spec is being refined based on feedback (managed by Xpec, not settable by agents).
- **READY** — Spec is written and approved, waiting for implementation.
- **IN_PROGRESS** — Someone is actively working on it.
- **COMPLETED** — Implementation is done.

## Tools Available

- `updateSpecStatus(id, status)` — Change a spec's status. Only accepts: READY, IN_PROGRESS, COMPLETED.
- `getSpecProgress(id, recentLimit?)` — Read the iteration log + current status. Use this to recover context before reading sections, whenever `recordedIterations > 0`.
- `recordSpecProgress(id, title, details, nextSteps)` — Append one iteration to the log. Iterations are immutable once recorded.
- `updateExposurePlan(id, content)` — Write or replace the spec's exposure plan (strategic level structure for the feature).
- `addSpecReview(specId, agentReview)` — Submit a one-way agent review of the spec quality.

## Instructions

### When resuming an in-progress spec

1. Look at `recordedIterations` returned by `listSpecifications` or `getFullSpecification`.
2. If `recordedIterations > 0`, call `getSpecProgress` BEFORE reading sections — regardless of the spec's status. The latest iteration's `nextSteps` is your resume point. The full iterations array (each with full markdown `details`) rebuilds the prior context.
3. If `recordedIterations === 0`, you're starting fresh — skip `getSpecProgress` and go straight to reading sections.

### When recording an iteration

Call `recordSpecProgress` once per coherent unit of work (typically one entry per level or major milestone — not per minor edit). Provide:

- **title** — short headline of what this iteration achieved (≤200 chars).
- **details** — markdown narrative (≤50KB). Recommended subsections (use as a guide, deviate when an iteration doesn't fit):
  - **State** — where things stand at the end of this iteration.
  - **Decisions** — technical/design decisions and their rationale.
  - **Delivered scope** — what was built, with file/component references.
  - **Tests** — what was tested and current status.
  - **Out of scope** — deliberately deferred items, with rationale.
  - **Open items** — cross-cutting items still being tracked. One bullet per item, prefixed with current state (`pending` / `RESOLVED` / `unchanged` / `NEW` / `observation`), brief context, and resolution trigger if applicable. Read the previous iteration's "Open items" and update each entry's state — do not re-debate items, just track their evolution.
- **nextSteps** — short, actionable resume pointer (≤500 chars).

### When authoring an exposure plan

If you ran `slice-this-feature` (or similar planning skill) and produced an exposure plan, call `updateExposurePlan(id, content)` to store it. The plan is replaceable: re-planning overwrites prior content. Humans can also edit it via the Xpec web UI.

### Reviews

Use `addSpecReview` only for a one-way review of spec quality (gaps, ambiguities, suggestions). It is NOT for progress tracking.

## Key Principle

The progress log is a living, immutable history of what the agent did and decided. Read it on resume, append to it at the close of each iteration. Architectural decisions that matter beyond this spec also belong in `CLAUDE.md` / ADRs / code comments so future agents on other specs find them; the iteration `details` is the moment of capture, the codebase is the durable home when applicable.
