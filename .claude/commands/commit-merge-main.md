---
description: Commit changes on the feature branch and merge into main
argument-hint: Short commit message describing the changes
allowed-tools: Read, Glob, Grep, Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git add:*), Bash(git commit:*), Bash(git checkout:*), Bash(git switch:*), Bash(git merge:*), Bash(git push:*)
---

You are helping to commit all current changes, merge the feature branch into main, and push. Always adhere to any rules or requirements set out in any CLAUDE.md files when responding.

User input: $ARGUMENTS

## High level behavior

Your job is to:

1. Stage and commit all relevant changes on the current feature branch
2. Merge the feature branch into `main`
3. Push `main` to the remote

## Step 1. Validate the branch

Check the current Git branch name. Abort if you are on `main` — tell the user to switch to a feature branch first.

## Step 2. Review changes

Run `git status` and `git diff` (staged + unstaged) to understand what will be committed. If there are no changes to commit, skip to Step 4 (merge).

## Step 3. Commit

- Stage all relevant changed and new files (avoid secrets like `.env`, credentials, etc.)
- Create a commit using `$ARGUMENTS` as the commit message subject
- Append ` ` to the commit message
- Use a HEREDOC to pass the commit message for correct formatting

## Step 4. Merge into main

- Switch to `main` with `git checkout main`
- Merge the feature branch into `main` (fast-forward when possible)
- If there are merge conflicts, stop and report the conflicts to the user — do NOT force resolve

## Step 5. Push main to remote

Push `main` to `origin`.

## Step 6. Final output

After the push completes, respond with a short summary:

```
Feature branch: <branch_name>
Commit: <short_sha> <commit_message>
Merged into: main
Pushed: origin/main
```
