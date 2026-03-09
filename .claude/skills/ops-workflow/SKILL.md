---
name: ops-workflow
description: Non-code workflow for research, strategy, content, and specs — never for planning or implementing code changes. Covers planning, clarification, execution, quality review, and state updates. Use only when the deliverable is NOT code (e.g., research briefs, content, specs, operational docs).
---

# Ops Workflow

Follow this process for all non-trivial non-code work.

**Scope:** This workflow produces strategy, research, content, and specs — not code. Plans should never include implementing changes in the app. We can produce content, briefs, and recommendations that the user takes to the coding repo.

## Complexity Judgment

Before starting, assess whether the task is **light** or **heavy**:

**Light** — a single deliverable, straightforward research, one or two state files to update:

- Research directly with Read/Grep/Glob/WebSearch
- Skip clarification if there is no ambiguity
- Single review pass

**Heavy** — multiple deliverables, cross-referencing multiple sources, multi-step analysis, or affects several state files:

- Launch parallel research agents for different aspects
- Always run clarification
- Structured review with explicit quality checks

When in doubt, lean toward heavy — the cost of extra diligence is low compared to shipping incomplete or inconsistent work.

## 1. Planning

Before doing any work, create a plan:

1. Check `backlog/` (start from `backlog/INDEX.md`) — if the task matches an existing backlog item, check for an existing draft plan linked from or stored alongside the item.
2. Run `/ops-plan <task description>` to start the planning workflow. This reads `MEMORY.md`, relevant `state/` and `references/` files, and `plans/completed/` for prior work — all before drafting the plan. If a draft plan exists in `backlog/`, use it as the starting point — move it to `plans/`, update the date and status to `active`, and refine it.
3. The skill creates (or activates) a dated plan file in `plans/` with an objective, proposed steps, and success criteria grounded in current project state.
4. Present the plan to the user for approval. Do not proceed until approved. Do NOT use `EnterPlanMode` — stay in the current permission mode throughout.

## 2. Clarification

After drafting the plan, ask clarifying questions before doing any work:

1. Use the **AskUserQuestion** tool with multi-select options to surface scope decisions, trade-offs, and assumptions.
2. Present concrete choices — don't ask open-ended questions when specific options are available. Group related decisions into a single question block (up to 4 questions per call).
3. If the task produces artifacts (copy, drafts, deliverables), clarify where they should be stored if not obvious. Default is `artifacts/` but the user may prefer a subfolder or different location.
4. Only skip this step if the task is absolutely straightforward and has no ambiguity.
5. Update the plan file with the user's answers before proceeding.

## 3. Execution

Carry out the plan:

1. Do the research, analysis, or writing described in the plan.
2. When researching, **always cite sources** — include URLs, document names, or specific references.
3. Store outputs in the appropriate location:
   - Research findings → `references/<topic>/`
   - Work products and deliverables → `artifacts/` (or as agreed in clarification step)
4. If the plan needs to change mid-execution (new information, blocked path), update the plan file and confirm the revised approach with the user before continuing.

## 4. Review

Before updating state, review the deliverables:

1. **Fact-check** — verify claims against cited sources. Flag any unsupported assertions.
2. **Consistency** — check that new artifacts don't contradict existing state files or prior completed plans.
3. **Completeness** — confirm the output covers everything the plan promised. If gaps remain, fill them or note them as out-of-scope with justification.
4. **Quality** — check formatting consistency, broken links, and missing references.

For heavy tasks, present a brief review summary to the user before proceeding to state updates.

## 5. State Updates

After execution, update project state:

1. **Complete the plan file** — fill in Outcome, Key Decisions, Artifacts, and Session Log sections.
2. **Update `backlog/`** — remove the completed item from the relevant file. If new tasks or ideas emerged during execution, add them to the appropriate file and section.
3. **Update `state/` files** — if the task changed the current state of anything documented in `state/`, update those files to reflect the new reality. Create a new state file if a significant new aspect of the project emerged.
4. **Update `MEMORY.md`** — if something significant changed about the project, update or add the relevant summary line and reference link.
5. **INDEX.md cascade check** — before finishing, list every file created, moved, renamed, or significantly changed during execution. For each one, confirm its folder's `INDEX.md` is up to date. If a folder's overall summary changed, cascade the update to the parent `INDEX.md`. Do not skip this step.

## 6. Cleanup

Before finishing, verify:

1. Move the plan to `plans/completed/` with a date prefix: `YYYY-MM-DD_original-filename.md`.
2. Confirm no stale plan files remain in `plans/` that should be in `completed/`.
3. All state files, INDEX.md files, and MEMORY.md are up to date.
4. Commit if the user asks.

Do not skip this step. If the conversation is ending and you haven't done this, do it now.
