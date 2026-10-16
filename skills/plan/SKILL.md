---
name: plan
description: Create an interview-driven, self-contained implementation plan from conversation requirements, optional local files, and repository evidence. Use when the user wants to plan work rather than implement it.
---

# Plan

Create an actionable implementation plan before changing code. The plan must contain enough context for a later session to execute it without repeating discovery. This skill plans work; it does not implement the plan.

## Inputs and boundaries

Use requirements already present in the conversation as the primary input. If the user provides one or more local requirements-file paths, read each file and combine its contents with the conversation. Treat a provided path as a complete path, including spaces; do not parse it as a tokenized identifier.

Relevant repositories and their checked-in guidance are also inputs when available. Do not require a ticket, a domain label, a team knowledge base, or a prescribed workspace layout.

During planning, do not modify application source, switch branches, pull remote changes, install dependencies, or otherwise mutate an affected repository unless the user explicitly requests it.

Follow the three phases below in order.

## Phase 1: Gather context

1. Summarize the requirements currently available from the conversation.
2. Read every explicitly supplied requirements file.
   - If a file is missing or unreadable, report the exact path problem and ask for a corrected path. Continue with sufficient conversation context when possible.
   - Reconcile file contents with the conversation. Call out meaningful conflicts and ask which source takes precedence rather than silently choosing one.
3. Identify the affected repository or repositories. If location or scope is unclear, ask the user before assuming a personal directory layout.
4. Read relevant checked-in project guidance, starting with files such as `AGENTS.md`, `CONTRIBUTING.md`, and `README.md`. Treat any provider-specific guidance only as context for that repository, never as a requirement of this skill.
5. Inspect the relevant code, tests, configuration, and existing documentation before asking questions that repository evidence can answer. When multiple repositories are affected, inspect each and record dependencies and a sensible execution order.
6. Select the plan output location:
   - Follow a plan location defined by the project guidance when one exists.
   - Otherwise, ask the user where to save the plan or propose a clear, descriptive local Markdown path.
   - If a plan already exists at the selected path, read it and ask whether to update it, replace it, or create a separate plan. Never overwrite it silently.

If neither the conversation nor supplied files provide enough context to begin, ask briefly for the problem statement and the relevant repository or path.

## Phase 2: Clarify requirements

Start by giving a concise summary of the understood problem, likely scope, affected repositories, and relevant code areas.

Then resolve uncertainty conversationally:

1. Answer questions from repository evidence yourself whenever possible.
2. Ask focused questions in small batches about only the remaining ambiguity. Useful topics include constraints, edge cases, compatibility, testing, rollout, dependencies, and completion criteria.
3. Follow up when an answer exposes material complexity or new decisions.
4. Do not turn the conversation into a mandatory form or questionnaire.
5. Stop when the work can be decomposed into concrete implementation tasks. Keep genuinely unresolved items as open questions in the plan.

Examples of situations to probe include error paths, retries, empty or invalid inputs, concurrency, existing callers, migration or rollback requirements, and the distinction between automated and manual verification.

## Phase 3: Write the plan

Write the selected Markdown file. Make it self-contained: a new implementation session should understand the purpose, affected areas, decisions, task order, and verification work without needing to repeat all discovery.

Use this structure when the sections add value; omit sections that would be empty or redundant:

```markdown
# <plan title>

**Purpose:** <why this work is needed>
**Status:** Draft
**Owner:** <owner, if known>
**Last updated:** <YYYY-MM-DD>

## Context

## Goals

## Non-goals

## Key Decisions

## Approach

## Tasks

## Testing and Verification

## Edge Cases

## Risks

## Open Questions
```

Write ordered, concrete tasks. Name likely files, components, interfaces, or repositories when known, state dependencies where relevant, and describe the intended change rather than using vague labels. Separate automated checks from manual verification. State uncertainty explicitly instead of inventing details.

When sensitive source material is encountered, include only what is necessary to perform the work; do not copy secrets or proprietary details into a plan intended for publication.

After writing the file, report:

- the plan path;
- a one-sentence summary of the approach; and
- that the plan is ready for a fresh implementation session.

Do not prescribe provider-specific commands or invocation syntax.
