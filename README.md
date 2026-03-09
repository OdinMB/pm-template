# PM Template

A project management repo structure designed for use with [Claude Code](https://claude.com/claude-code). Organizes strategy, research, content, and operational planning into a convention-based folder layout that Claude can navigate and maintain autonomously.

This is **not** a code repo. It produces research briefs, marketing copy, grant applications, specs, pitches, and other non-code deliverables — using structured workflows, plan tracking, and living state documents.

## Quick Start

1. **Clone or copy** this repo into your project:

   ```bash
   # As a standalone repo
   git clone https://github.com/YOUR_USERNAME/pm-template.git my-project-pm
   cd my-project-pm

   # Or as a subfolder inside an existing code repo
   cp -r pm-template/ my-app/pm/
   ```

2. **Fill in the blanks:**
   - `MEMORY.md` — Add your project name, description, constraints, and goals.
   - `CLAUDE.md` — Replace `[PROJECT NAME]` in the first line. Adjust the working directory section if this repo lives inside another repo.
   - `state/INDEX.md` — Start documenting your project's current reality.
   - `backlog/INDEX.md` — Add your first prioritized tasks.

3. **Start working** by opening Claude Code in the repo directory. Use `/workflow` to kick off any non-trivial task.

## Folder Structure

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

## Workflows & Commands

### Core Workflows

| Command | What it does |
|---------|-------------|
| `/workflow` | Full PM workflow: plan → clarify → execute → review → update state. Use for any non-trivial task. |
| `/work-plan <task>` | Create a plan file without executing it. Good for scoping work before committing to it. |
| `/executive-overview` | Read-only synthesis of state + backlogs. Answers "what should we do next?" |

### Batch Operations

| Command | What it does |
|---------|-------------|
| `/ops-batch-plan` | Write multiple plans in one session without stopping for input. |
| `/ops-batch-execute` | Execute multiple plans in one session without stopping for input. |

### Code Workflows (if paired with a code repo)

| Command | What it does |
|---------|-------------|
| `/batch-plan` | Batch-write code implementation plans. |
| `/batch-implement` | Batch-implement code plans with TDD. |
| `/tdd` | Enforce test-driven development. |

### Maintenance

| Command | What it does |
|---------|-------------|
| `/tidy-plans` | Move completed plans to `plans/completed/` with date prefixes. |

## Key Conventions

### INDEX.md Hierarchy

Every folder has an `INDEX.md` that provides a complete overview at that level of abstraction. Claude reads the INDEX first and drills down only when needed. When you create, rename, or significantly change a file, update the folder's INDEX — and cascade upward if the parent's summary changed too.

### State vs. Backlog

- **State** = present reality. "We have 200 subscribers." "EAIF rejected our grant."
- **Backlog** = future actions. "Apply to NLnet by April 1." "Research podcast hosting options."

When something is done, it moves from backlog to state. Passed opportunities move to references (under a "Passed / Not Pursuing" heading), not a backlog graveyard.

### Plans → Artifacts → References

- **Plans** log the process (what steps, what decisions, what outcome).
- **Artifacts** are the deliverables (the submitted application, the published post).
- **References** are the inputs (the research that informed the decision).

A plan links to its artifacts. An artifact stands alone. Don't put deliverable text in plan files.

### Waiting-For Markers

Mark blocked items inline: `WAITING (grant committee, since 2026-03-01)`. The `/executive-overview` command greps for these and surfaces them automatically.

### Living Document Dates

State files, backlogs, and MEMORY.md include `_Last updated: YYYY-MM-DD_` near the top. Update the date whenever you edit.

## Customization

### Adapting for Your Project

The template is intentionally generic. Common customizations:

- **Add backlog subfolders** for your project's areas (e.g., `backlog/marketing/`, `backlog/fundraising/`).
- **Add reference subfolders** for research topics (e.g., `references/competitors/`, `references/legal/`).
- **Add artifact subfolders** for deliverable types (e.g., `artifacts/grants/`, `artifacts/pitches/`).
- **Add state files** as your project develops (e.g., `state/funding.md`, `state/audience/`).

### Pairing with a Code Repo

If this PM repo lives inside a code repo (e.g., `my-app/pm/`):

1. Update the working directory section in `CLAUDE.md` to reference the parent (e.g., `../client/`, `../server/`).
2. Add the PM folder's scope constraint to the parent repo's `CLAUDE.md`: "Never write, edit, or create files in `pm/`. Read only."
3. The `/batch-plan` and `/batch-implement` commands are designed for the code repo context — they reference `/workflow` which resolves to the code development workflow at user level.

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- Git (for plan tracking and batch operation branching)
