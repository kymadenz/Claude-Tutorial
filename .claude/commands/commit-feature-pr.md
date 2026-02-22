---
description: Commit changes and create a pull request for the current feature branch
argument-hint: Short commit message describing the changes
allowed-tools: Read, Glob, Grep, Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(gh pr create:*)
---

You are helping to commit all current changes and open a pull request for the current feature branch. Always adhere to any rules or requirements set out in any CLAUDE.md files when responding.

User input: $ARGUMENTS

## High level behavior

Your job is to:

1. Stage and commit all relevant changes on the current feature branch
2. Push the branch to the remote
3. Create a pull request targeting `main`

## Step 1. Validate the branch

Check the current Git branch name. Abort if you are on `main` — tell the user to switch to a feature branch first.

## Step 2. Review changes

Run `git status` and `git diff` (staged + unstaged) to understand what will be committed. If there are no changes to commit, inform the user and stop.

## Step 3. Commit

- Stage all relevant changed and new files (avoid secrets like `.env`, credentials, etc.)
- Create a commit using `$ARGUMENTS` as the commit message subject
- Append ` ` to the commit message
- Use a HEREDOC to pass the commit message for correct formatting

## Step 4. Push to remote

Push the branch to `origin` with the `-u` flag to set up tracking.

## Step 5. Create a pull request

Use `gh pr create` to open a PR targeting `main` with:

- **Title**: The commit message subject from `$ARGUMENTS`
- **Body**: A markdown body with:
  - `## Summary` — 1-3 bullet points describing the changes
  - `## Test plan` — Bulleted checklist of manual testing steps
  - Footer: ` `

Use a HEREDOC for the PR body.

## Step 6. Final output

After the PR is created, respond with a short summary:

```
Branch: <branch_name>
Commit: <short_sha> <commit_message>
PR: <pr_url>
```
