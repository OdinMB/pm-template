# PM Template

A project management repo template designed for use with [Claude Code](https://claude.com/claude-code). Organizes strategy, research, content, and operational planning into a convention-based folder layout that Claude can navigate and maintain autonomously.

This is **not** a code repo. It produces research briefs, marketing copy, grant applications, specs, pitches, and other non-code deliverables — using structured workflows, plan tracking, and living state documents.

## Quick Start

1. **Fork or clone** this repo:

   ```bash
   git clone https://github.com/YOUR_USERNAME/pm-template.git my-project-pm
   cd my-project-pm
   ```

2. **Run `/ops:scaffold`** in Claude Code. It will interview you about your project and create the full folder structure, `CLAUDE.md`, `MEMORY.md`, and initial `INDEX.md` files.

3. **Start working** with `/ops:handle` to kick off any non-trivial task.

## What You Get

This template ships with ops-specific Claude Code skills and commands:

- **`/ops:handle`** — Plan and execute a task end-to-end (delegates to `/ops-plan` + `/ops-execute`)
- **`/ops:scaffold`** — Set up (or adjust) the folder structure interactively
- **`/ops:overview`** — Synthesize project state into a ranked action plan
- **`/ops:batch-plan`** / **`/ops:batch-execute`** — Batch operations without user input
- **`/ops:get-to-work`** — Autonomous ops work loop (run before stepping away)
- **`/ops:housekeeping`** — Consistency check for INDEX.md hierarchy, stale dates, and orphaned files
- **`/review-followup`** — Process follow-up files from autonomous runs
- **`/tidy-plans`** — Move completed plans to `plans/completed/` with date prefixes

## Folder Structure (after scaffolding)

```
├── state/          # What currently exists (living documents)
├── backlog/        # What to do next (prioritized tasks)
├── references/     # Research inputs (read-only context)
├── artifacts/      # Deliverables produced (applications, copy, specs)
├── plans/          # Active plans being executed
│   └── completed/  # Archived plans with outcomes
├── CLAUDE.md       # Repo instructions for Claude Code
└── MEMORY.md       # Project context (always loaded)
```

Each folder has an `INDEX.md` that serves as the entry point — read the INDEX before diving into individual files.

## Key Conventions

### State vs. Backlog

- **State** = present reality. "We have 200 subscribers." "EAIF rejected our grant."
- **Backlog** = future actions. "Apply to NLnet by April 1." "Research podcast hosting options."

When something is done, it moves from backlog to state.

### Plans → Artifacts → References

- **Plans** log the process (what steps, what decisions, what outcome).
- **Artifacts** are the deliverables (the submitted application, the published post).
- **References** are the inputs (the research that informed the decision).

### Pairing with a Code Repo

If this PM repo lives inside a code repo (e.g., `my-app/pm/`), `/ops:scaffold` will adjust the working directory and scope sections automatically.

## Requirements

- [Claude Code](https://claude.com/claude-code) (CLI, Desktop, or Cowork)
- Git (for plan tracking and batch operation branching)
