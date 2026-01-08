Retrieve documentation from GitHub repositories. Use GitHub API with base64 decoding (never WebFetch).

**Find doc files:**
```bash
BRANCH=$(gh api repos/{owner}/{repo} --jq '.default_branch')
gh api "repos/{owner}/{repo}/git/trees/$BRANCH?recursive=1" --jq '
  .tree[] | select(.type == "blob") |
  select(.path | test("\\.(md|mdx|txt|rst|rdoc)$"; "i")) |
  select(.path | test("CODE_OF_CONDUCT|CONTRIBUTING|LICENSE|CLAUDE\\.md|/blog/|robots\\.txt|llms.*\\.txt") | not) |
  .path'
```

**Read single file:**
```bash
gh api repos/{owner}/{repo}/contents/{path} --jq '.content' | base64 -d
```

**Read all docs:**
```bash
# Pipe file list to: while IFS= read -r f; do echo "=== $f ==="; gh api "repos/{owner}/{repo}/contents/$f" --jq '.content' | base64 -d; done
```

Retrieve selectively based on user's request, or all if asked to "become an expert" or "read everything".
