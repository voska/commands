Check PR #$ARGUMENTS for review comments and make necessary fixes.

Install extension if needed: `gh extension install agynio/gh-pr-review`

**Fetch unresolved review comments:**
```bash
gh pr-review review view $ARGUMENTS --unresolved --not_outdated
```

**Workflow:**
1. Fetch comments using command above
2. Fix each issue at the specified `path:line`
3. Push changes
4. Resolve threads: `gh pr-review threads resolve $ARGUMENTS --thread-id <THREAD_ID>`
