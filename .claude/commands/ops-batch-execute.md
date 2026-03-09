---
description: Execute a batch of ops plans continuously without user input, storing any issues and user questions in a .md file to be processed with the user afterwards. Do NOT invoke this yourself! Should only be invoked by the user.
---

# Task

You will be going on a plan execution spree for non-code work. I will provide a list of plans. Execute these plans one by one without interruptions.

# Steps

1. Create a new branch for your work. This makes it easy to discard the entire session if something goes wrong.
2. Create a follow-up .md file in the `plans/` directory (or wherever plan files are stored) with three sections: user input needed, files to be deleted, and execution issues. You will process that file with the user when you're done executing the plans.
3. Execute the plans one after the other. Don't stop for user inputs. Simply record what you need from the user in the follow-up file and move on.
4. After all plans are executed, go through the follow-up items with the user (user decisions, execution notes, state update questions). Document each resolved item in the related completed plan file.
5. When all follow-up items are resolved, confirm with the user to merge the branch back into the main branch. Before the merge, make sure that the follow-up file contains no information that isn't already recorded in a plan file, and that all items have been resolved. Then delete the follow-up file and perform the merge.

# Guidelines

## Record actions that need the user and move on

- Do not stop for any user input.
- If you need input from the user to execute a plan, skip that plan, record the questions in the follow-up file, and move on to the next item.
- If you want to delete a file, don't! Instead, record it in the follow-up file. That way, you don't need user confirmation which would block the process.

## Execute plans by following `/ops-workflow`

- Do the research, analysis, or writing described in each plan.
- Always cite sources when researching.
- Run the review step (fact-check, consistency, completeness, quality).
- Update state files, backlog, INDEX.md cascade, and MEMORY.md.
- Respect the bash command rules from CLAUDE.md so the process doesn't get interrupted for user confirmations.
- Don't look ahead into future plans, and don't execute plans in parallel. One plan after the other.

## Move plan, then commit

After completing each plan:

1. Fill in the plan's Outcome, Key Decisions, Artifacts, and Session Log sections.
2. Move the plan file from `plans/` to `plans/completed/` with a date prefix: `YYYY-MM-DD_original-filename.md`.
3. Then commit all changes (artifacts + state updates + completed plan) with a descriptive message.

Do this after every plan — don't batch commits across multiple plans.
