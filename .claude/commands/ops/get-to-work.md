---
description: Autonomous ops work — identifies, prioritizes, and executes tasks in a loop without user input. Creates a branch with commits for each completed task and a follow-up file for review. Run this before stepping away from an ops repo.
---

# Get to Work

You will autonomously advance this ops project. Follow the `autonomous-conventions` skill throughout — the entire process runs without user input.

## Safety Constraints

**No real-world actions.** You must NEVER:

- Send emails, messages, or notifications
- Submit forms, applications, or registrations
- Post to social media or external platforms
- Make API calls that modify external state
- Make purchases or financial transactions
- Contact anyone on behalf of the user

You CAN: research (web search, read public pages), write files, create plans, analyze data, produce drafts and artifacts the user can later use for world-affecting actions, and maintain the repo's knowledge system.

## Phase 1: Setup

1. Determine today's date and create a new branch: `YYYY-MM-DD-get-to-work`
2. Create a follow-up file at `plans/YYYY-MM-DD_get-to-work-followup.md`:

```markdown
# Get to Work — Follow-up

## Controversial Decisions
Items where the agent made a judgment call the user should review.

## Skipped Items
Opportunities identified but not acted on, with reasons.

## User Input Needed
Questions that blocked progress on specific items.

## Implementation Issues
Problems encountered during execution.

## Cycle Log
Summary of each identify → prioritize → execute cycle.
```

## Phase 2: Load Context

Gather the project overview without producing terminal output. Read these files (skip any that don't exist):

1. `MEMORY.md` — project overview and knowledge map
2. `state/INDEX.md` → then every file listed in it
3. `backlog/INDEX.md` → then every file and subfolder listed in it
4. `plans/INDEX.md` → then every active plan (not completed)
5. `plans/completed/INDEX.md` — scan the 5 most recent completed plans

Build a mental model of: what the project is trying to achieve, where things stand, what's already planned, and what was recently done. You'll use this context throughout.

## Phase 3: Work Cycle

Repeat this cycle until one of the stopping conditions (Phase 4) is met.

**Core duty: your job is to find and do useful work.** If the current backlog is full of blocked items, that means you need to generate new items — not stop. Research, state refreshes, content drafts, consistency fixes, and knowledge-gap analysis are always available. "Everything is blocked" means the backlog needs new entries, not that you're done.

### Step 1: Identify New Work

Follow the `ops-find-work` skill:

- Scan the project through all applicable lenses (goal gaps, stale state, research opportunities, content gaps, follow-through, consistency)
- Add new backlog entries for anything valuable that isn't already tracked
- Specifically look for work an autonomous agent can complete: research, writing, analysis, state updates, drafts, knowledge management. Every project has stale information to refresh, knowledge gaps to fill, and drafts to prepare — find them.
- Record what was added in the Cycle Log section of the follow-up file
- Commit the backlog updates: `"identify work: add N new backlog items (cycle M)"`

On the first cycle, do a thorough scan across all lenses. On subsequent cycles, start with follow-through from the tasks just completed, but if that yields fewer than 3 new items, widen to a full scan across all lenses. The backlog should never run dry — if it does, you haven't looked hard enough.

**Escalation**: If your full-lens scan (lenses 1-6) yields fewer than 2 new feasible items, that means the project's existing structure has been well-mined — it does NOT mean you're done. Spawn a **strategist sub-agent** to open up new directions:

```
Read the strategist agent instructions at: agents/strategist.md

Project context:
- MEMORY.md location: [path to MEMORY.md]
- State files: [list key state files]
- Current backlog items: [summarize what's already tracked]
- Recent completed work: [summarize last 3-5 completed plans]
- What lenses 1-6 found (or didn't): [brief summary]

Your job: identify 3-5 new directions of work this project should explore.
Stay grounded in the project's goals and limitations from MEMORY.md.
Every suggestion must be something an autonomous agent can start working on.
```

Add the strategist's output items to the backlog and continue the cycle. The project benefits most from autonomous work precisely when it opens up territory the owner hasn't had time to explore themselves.

### Step 2: Prioritize

Follow the `ops-prioritize` skill:

- Score all candidate tasks (active plans + backlog items + newly added items)
- Select 2-3 independent, feasible, high-impact tasks
- Prepare execution briefs for each
- Record the selection and reasoning in the Cycle Log

**If prioritization yields zero feasible tasks**: this is not a stopping condition. Go back to Step 1 immediately and run a full-lens scan focused on generating agent-feasible work. The problem is that your backlog doesn't contain enough autonomous-friendly items — fix the backlog, don't stop the cycle.

### Step 3: Execute Tasks

Execute the selected tasks one at a time using sub-agents. For each task, spawn a sub-agent with these instructions:

```
You are executing an ops task autonomously. Follow these rules strictly:

**Skills to follow:**
- `ops-execute` — for execution, review, state updates, insight harvesting, and plan archiving (skip its "confirm with user" steps since this is autonomous)
- `autonomous-conventions` — for autonomous execution rules

**Safety constraints — NEVER:**
- Send emails, messages, or notifications
- Submit forms, applications, or registrations
- Post to social media or external platforms
- Make API calls that modify external state
- Contact anyone on behalf of the user

**You CAN:** research (web search, read public pages), write files, create plans, analyze data, produce drafts the user can act on later, and maintain the repo's knowledge system.

**Your task:**
[Insert the execution brief from the prioritization step]

**Process:**
1. If no plan file exists for this task, create one in plans/ following ops-plan format
2. Use the `/ops-execute` skill to execute the plan
3. For borderline insights or suggested backlog items you're unsure about, add them to the follow-up file instead of persisting directly

**If you get stuck or need user input:**
- Record the question or blocker in plans/YYYY-MM-DD_get-to-work-followup.md under "User Input Needed"
- Make a reasonable assumption and proceed, noting your assumption under "Controversial Decisions"
- Only skip a task entirely if proceeding would be genuinely harmful or produce useless output

**When done:** Summarize what you accomplished, what files you created/modified, and any items you added to the follow-up file.
```

After each sub-agent completes:

1. Review its summary for anything that should go in the follow-up file
2. Verify the sub-agent actually persisted insights: check if MEMORY.md or backlog files were updated when the task involved research or analysis. If the sub-agent produced findings but didn't persist them, do it now.
3. Commit all changes with a descriptive message: `"[task-slug]: [what was done]"`
4. Note the completed task in the Cycle Log

### Step 4: Assess & Loop

After completing all tasks in a cycle:

1. Re-read any state files or backlog files that were modified during execution
2. Check if the stopping conditions (Phase 4) are met
3. If not, return to Step 1 for the next cycle

## Phase 4: Stopping Conditions

Keep cycling. The default is to **keep going**, not to stop.

You stop ONLY when:

- **User-specified cutoff**: if the user provided a task limit or time constraint in $ARGUMENTS, respect it
- **Hard block**: ALL of the following must be true simultaneously:
  1. Every candidate task in the current backlog requires real-world actions or is blocked on user input
  2. You ran `ops-find-work` with a **full scan across ALL lenses** (goal gaps, stale state, research opportunities, content gaps, follow-through, consistency) — not just follow-through
  3. You spawned the **strategist agent** (`agents/strategist.md`) and it produced zero feasible items even after considering adjacent opportunities, strategic gaps, and preparatory research
  4. That combined effort produced zero new feasible items that an autonomous agent could work on
  5. You have already completed at least one full identify→prioritize→execute cycle in this session

Before declaring a hard block, verify each condition. If you only checked follow-through in Step 1, go back and run the full lens sweep. If you haven't spawned the strategist agent yet, do that before stopping — it's specifically designed to generate work when everything else is exhausted.

These are NOT reasons to stop:
- "Diminishing returns" — small tasks are still valuable
- "The backlog is empty" — generate more items
- "Most items are blocked" — generate new ones that aren't
- "Remaining items require user action" — that describes the *current* backlog, not all possible work. Find new work.

When a stopping condition is met, proceed to Phase 5.

## Phase 5: Summary & Handoff

Create `plans/YYYY-MM-DD_get-to-work-summary.md`:

```markdown
# Get to Work — Summary

**Date:** YYYY-MM-DD
**Branch:** YYYY-MM-DD-get-to-work
**Cycles completed:** N

## What Was Done

| # | Task | Cycle | Status | Commit | Artifacts |
|---|------|-------|--------|--------|-----------|
| 1 | [task name] | 1 | completed | abc1234 | [files created] |
| 2 | [task name] | 1 | completed | def5678 | [files created] |
| 3 | [task name] | 2 | completed | ghi9012 | [files created] |
| ... | ... | ... | ... | ... | ... |

## New Backlog Items Added
[List of items added during identify-work phases that weren't executed]

## Stats
- Tasks completed: N
- Plans created: N
- State files updated: N
- Backlog items added: N
- Backlog items completed: N

## Stopping Reason
[Why the agent stopped cycling]

## Follow-up Required
[Summary of items from follow-up file, grouped by urgency]
```

Commit the summary: `"get-to-work: summary and follow-up (N tasks completed across M cycles)"`

### Handoff

When the user returns, present the summary and use the `/review-followup` skill to walk them through the follow-up file. After follow-up items are resolved, offer to merge the branch.
