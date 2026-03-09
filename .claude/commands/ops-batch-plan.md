---
description: Create a batch of ops plans continuously without user input, storing any user questions in a .md file to be processed with the user afterwards. Do NOT invoke this yourself! Should only be invoked by the user.
---

# Task

You will be going on a plan writing spree for non-code work. I will provide a list of tasks or ideas. Write an ops plan for each of these items without interruptions.

# Guidelines

- Create a follow-up .md file in the `plans/` directory (or whatever the project uses for plan files). You will process that file with the user when you're done writing the initial versions of the plans.
- Filenames of plans should reference the goal of the plan, prefixed with today's date: `YYYY-MM-DD-<slug>.md`.
- Give plan files an additional numeric prefix to indicate implementation order. (`01-`, `02-`, etc.)
- Do not stop for any user input.
- Record any clarifications and decisions that you need from the user in the follow-up file.
- In the plan files, list the options that the user will choose from later and any open questions that the user still has to answer.
- You can write plans in parallel if they don't directly relate to each other.
- **Scope check**: Plans must never include implementing changes in app codebases. This workflow produces content, research, specs, and briefs — not code.
- Use the plan file format from `/ops-plan` (objective, steps, artifacts, files to create/modify, success criteria, plus blank outcome sections).

Once you're done generating the initial versions of the plans, collect answers to the open questions from the user and adjust the plan files based on the responses.

# Cleanup

After all questions are resolved and plans are finalized, integrate any remaining follow-up items (resolved decisions, execution order, clarifications) into the plan files they relate to. Each plan file should be self-contained — the follow-up file should contain no information that isn't already recorded in a plan file. Then delete the follow-up file.
