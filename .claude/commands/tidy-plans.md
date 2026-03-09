---
description: Move completed plan files to the completed/ subdirectory with date prefixes. Run this to clean up stale plans.
allowed-tools: Read, Glob, Grep, Bash(ls *), Bash(mv *), Bash(git log *)
---

# Task

Scan the project's plan directory for completed plan files and move them to the `completed/` subdirectory with the correct date prefix. Fix nonsensical filenames along the way.

# Steps

1. **Find the plan directory.** Check for `.plans/` at the repo root. If it doesn't exist, check for `plans/`. If neither exists, tell the user and stop.

2. **Find the completed subdirectory.** It should be `<plan-dir>/completed/`. If it doesn't exist, create it.

3. **Read each plan.** Read every `.md` file in the plan directory (not in subdirectories). For each plan, determine:
   - What the plan's goal is (from its `#` heading and content)
   - What files it lists as modified/created (from "Files to Modify", "Files Changed", or similar sections)

4. **Check if the plan is completed.** Try each method in order — stop at the first match:

   a. **Explicit status markers** (fast — check first):
      - `Status: completed` or `Status: done` field in the plan
      - All success criteria checkboxes are checked (`- [x]`)
      - Outcome section is filled in (not `_Fill in when completed._` or blank)

   b. **Git history check** (use when no explicit markers exist):
      - Extract the key file paths from the plan's "Files to Modify" / "Files Changed" / "Changes" sections.
      - Run `git log --oneline --after="YYYY-MM-DD" -- <file1> <file2> ...` using the files listed in the plan. Use the plan file's own modification date or a reasonable lookback window (e.g. 30 days).
      - Look for commits whose messages plausibly match the plan's goal.
      - If a matching commit exists, the plan is **completed**. Use that commit's date as the completion date.
      - If the plan lists files but none have been touched in git, it's **not completed**.

   c. **No files listed, no status markers**: Mark as "possibly completed — check manually" and skip.

5. **Check for clearly active plans.** Never move a plan that:
   - Has `Status: active` or `Status: in-progress`
   - Has unchecked success criteria checkboxes (`- [ ]`)
   - Has an "Open Questions" section with unresolved items and no git evidence of implementation

6. **Fix nonsensical filenames.** Before moving, check if the filename reflects the plan's goal:
   - Read the plan's `# heading` (the first H1).
   - If the filename is clearly unrelated to the heading — derive a new kebab-case filename from the heading.
   - Keep the `.md` extension. Keep any existing date prefix.
   - Use short, descriptive kebab-case: lowercase, hyphens, no filler words.

7. **Determine the date prefix.** In priority order:
   - The date of the matching git commit (from step 4b)
   - The plan's `Date` field if present
   - Today's date as fallback
   - Format: `YYYY-MM-DD_`

8. **Skip plans that already have a date prefix.** If the filename already matches `YYYY-MM-DD_*` or `YYYY-MM-DD-*`, don't add another prefix — just move it as-is (still apply the rename if the rest of the name is nonsensical).

9. **Move each completed plan** to `<plan-dir>/completed/<date-prefix>_<final-filename>`.

10. **Report results.** Show a table with columns: original filename, new filename (if renamed), status, and date used. Group into:
    - **Moved**: files moved to `completed/`
    - **Skipped (active)**: files that are clearly still in progress
    - **Check manually**: files where completion couldn't be determined

# Guidelines

- Do not modify plan file contents — only move/rename them.
- When checking git history, keep queries focused: use the 2-4 most distinctive file paths from the plan, not every file mentioned.
- A plan that lists files and ALL of those files have relevant commits is strong evidence of completion. A plan where only some files were touched is ambiguous — list as "check manually".
- If unsure whether a plan is completed, skip it and list it as "possibly completed — check manually".
- Never move files that are clearly still active.
- When renaming, confirm the new name is unambiguous within the completed directory (no collisions).
