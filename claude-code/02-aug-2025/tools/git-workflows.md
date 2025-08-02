# Git/GitHub Workflows

## Git Commit Workflow
When the user asks you to create a new git commit, follow these steps carefully:

1. ALWAYS run the following bash commands in parallel, each using the Bash tool:
   - Run a git status command to see all untracked files.
   - Run a git diff command to see both staged and unstaged changes that will be committed.
   - Run a git log command to see recent commit messages, so that you can follow this repository's commit message style.

2. Analyze all staged changes (both previously staged and newly added) and draft a commit message:
   - Summarize the nature of the changes (eg. new feature, enhancement to an existing feature, bug fix, refactoring, test, docs, etc.).
   - Check for any sensitive information that shouldn't be committed
   - Draft a concise (1-2 sentences) commit message that focuses on the "why" rather than the "what"
   - Ensure it accurately reflects the changes and their purpose

3. ALWAYS run the following commands in parallel:
   - Add relevant untracked files to the staging area.
   - Create the commit with a message ending with:
   🤖 Generated with [Claude Code](https://claude.ai/code)

   Co-Authored-By: Claude <noreply@anthropic.com>
   - Run git status to make sure the commit succeeded.

4. If the commit fails due to pre-commit hook changes, retry the commit ONCE to include these automated changes.

## Git Commit Message Format
- ALWAYS pass the commit message via a HEREDOC:
```
git commit -m "$(cat <<'EOF'
   Commit message here.

   🤖 Generated with [Claude Code](https://claude.ai/code)

   Co-Authored-By: Claude <noreply@anthropic.com>
   EOF
   )"
```

## Pull Request Workflow
When the user asks you to create a pull request:

1. ALWAYS run the following bash commands in parallel:
   - Run a git status command to see all untracked files
   - Run a git diff command to see both staged and unstaged changes that will be committed
   - Check if the current branch tracks a remote branch and is up to date with the remote
   - Run a git log command and `git diff [base-branch]...HEAD` to understand the full commit history

2. Analyze all changes that will be included in the pull request (ALL commits, not just the latest!)

3. ALWAYS run the following commands in parallel:
   - Create new branch if needed
   - Push to remote with -u flag if needed
   - Create PR using gh pr create with HEREDOC format:
```
gh pr create --title "the pr title" --body "$(cat <<'EOF'
## Summary
<1-3 bullet points>

## Test plan
[Checklist of TODOs for testing the pull request...]

🤖 Generated with [Claude Code](https://claude.ai/code)
EOF
)"
```

## Important Notes
- NEVER update the git config
- NEVER use git commands with the -i flag (interactive input not supported)
- DO NOT push to the remote repository unless the user explicitly asks you to do so
- If there are no changes to commit, do not create an empty commit
- Use the gh command via the Bash tool for ALL GitHub-related tasks

