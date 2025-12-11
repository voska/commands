Rename the current Git branch to follow the Conventional Branch specification.

## Conventional Branch Format
`<type>/<description>`

## Branch Types
- `feature/` or `feat/` - New features
- `bugfix/` or `fix/` - Bug corrections
- `hotfix/` - Urgent production fixes
- `release/` - Version release preparation
- `chore/` - Non-code tasks (deps, docs)

## Naming Rules
1. Lowercase letters (a-z), numbers (0-9), hyphens (-) only
2. Dots permitted only in release versions (e.g., `release/v1.2.0`)
3. No consecutive hyphens/dots, none at start/end
4. Include ticket numbers when applicable (e.g., `feature/issue-123-login`)

## Instructions

1. Get the current branch name using `git branch --show-current`
2. If already on `main` or `master`, inform user and exit
3. Analyze the current branch name and any provided arguments: $ARGUMENTS
4. Determine the appropriate branch type based on:
   - User-provided type in arguments
   - Keywords in current branch name (fix, bug, feature, hotfix, release, chore)
   - Ask user if type cannot be determined
5. Generate a new branch name following the spec
6. Show the user the proposed rename: `current-name` → `new-name`
7. Ask for confirmation before renaming
8. Rename using: `git branch -m <new-name>`
9. If the branch has a remote, warn user they may need to update it with:
   ```
   git push origin -u <new-name>
   git push origin --delete <old-name>
   ```

## Examples
- `my-login-feature` → `feature/login`
- `fix-header-bug` → `fix/header-bug`
- `JIRA-123-auth` → `feature/jira-123-auth`
- `urgent-security-patch` → `hotfix/security-patch`
