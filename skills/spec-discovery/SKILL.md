---
name: spec-discovery
description: How to discover and navigate Xpec specifications. Use when the user asks to find, list, or browse specifications, or when you need to understand what specs are available before starting work.
---

# Specification Discovery

## Purpose

Guide the agent through discovering available specifications in an Xpec workspace. Specifications are the source of truth for what needs to be built.

## Tools Available

- `listSpecifications` — List specs with optional filters (`status`, `projectId`, `limit`). Returns metadata and available section slugs, but no content.
- `getSpecificationSections` — Retrieve specific sections by slug. Use this for targeted reading.
- `getFullSpecification` — Retrieve the entire spec. Avoid unless you truly need everything.

## Instructions

1. **Start with `listSpecifications`** to see what's available. Use filters when possible:
   - `status: "READY"` — specs ready to be worked on
   - `status: "IN_PROGRESS"` — specs currently being implemented
   - `projectId` — narrow to a specific project

2. **Note the section slugs** returned for each spec. These tell you what content is available (e.g., `overview`, `user-stories`, `wireframes`, `acceptance-criteria`).

3. **Read only what you need** using `getSpecificationSections` with specific slugs. Do not fetch the full spec unless the user explicitly asks for it or the task requires all sections.

4. **Present findings clearly** — show the user spec titles, statuses, and available sections so they can decide what to explore further.

## Key Principle

Always prefer progressive discovery: list first, then read specific sections. This keeps context usage minimal and responses focused.
