---
description: Execute a batch of ops plans continuously without user input, storing any issues and user questions in a .md file to be processed with the user afterwards. Do NOT invoke this yourself! Should only be invoked by the user.
---

# Task

You will be going on a plan execution spree for non-code work. I will provide a list of plans. Execute these plans one by one without interruptions.

Follow the `autonomous-conventions` skill throughout.

# Steps

1. Create a new branch for your work.
2. Create a follow-up file per the `autonomous-conventions` skill.
3. Execute the plans one after the other. Don't look ahead into future plans, and don't execute plans in parallel.
4. After all plans are executed, use the `/review-followup` skill to walk through follow-up items with the user.
5. When all follow-up items are resolved, confirm with the user to merge the branch. Then perform the merge.

# Execution

For each plan, use the `/ops-execute` skill. After it completes, commit all changes (artifacts + state updates + completed plan) with a descriptive message.

Don't batch commits across multiple plans — one commit per plan.
