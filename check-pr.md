Check PR #$ARGUMENTS for review comments and make necessary fixes.

**Steps:**
1. Use `gh api` to fetch inline review comments, general comments, and review summaries
2. Analyze feedback and identify required changes
3. Implement fixes
4. Push changes

**Key commands:**
```bash
# Inline comments (most important - specific code feedback)
gh api "repos/{owner}/{repo}/pulls/$PR_NUM/comments"

# General PR comments
gh api "repos/{owner}/{repo}/issues/$PR_NUM/comments"

# Review summaries
gh api "repos/{owner}/{repo}/pulls/$PR_NUM/reviews"
```

Focus on inline review comments first as they point to specific lines needing changes.
