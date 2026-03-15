---
description: Create a batch of ops plans continuously without user input, storing any user questions in a .md file to be processed with the user afterwards. Do NOT invoke this yourself! Should only be invoked by the user.
---

# Task

You will be going on a plan writing spree for non-code work. I will provide a list of tasks or ideas. Write an ops plan for each of these items without interruptions.

Follow the `autonomous-conventions` skill throughout.

# Guidelines

- Create a follow-up file per the `autonomous-conventions` skill.
- Filenames of plans should reference the goal of the plan, prefixed with today's date: `YYYY-MM-DD-<slug>.md`.
- Give plan files an additional numeric prefix to indicate implementation order. (`01-`, `02-`, etc.)
- Record any clarifications and decisions that you need from the user in the follow-up file.
- In the plan files, list the options that the user will choose from later and any open questions that the user still has to answer.
- You can write plans in parallel if they don't directly relate to each other.
- **Scope check**: Plans must never include implementing changes in app codebases. This workflow produces content, research, specs, and briefs — not code.
- Use the plan file format from `/ops-plan` (objective, steps, artifacts, files to create/modify, success criteria, plus blank outcome sections).

# Review

Once all plans are written, use the `/review-followup` skill to walk through the follow-up file with the user. After each item is resolved, integrate the decision into the relevant plan file so each plan is self-contained. Then delete the follow-up file.
