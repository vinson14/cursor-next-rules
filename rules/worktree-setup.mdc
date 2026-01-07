---
description: Apply when setting up or working with git worktrees. Covers worktree.json configuration for automated setup commands including dependency installation and environment file copying.
globs:
    - "**/worktree.json"
alwaysApply: false
---

# Worktree Setup for Next.js

Create a `worktree.json` file in the root of your repository with setup commands that run automatically when creating a new worktree.

## Example `worktree.json`

```json
{
    "setup-worktree": [
        "pnpm install --frozen-lockfile",
        "cp $ROOT_WORKTREE_PATH/.env.local .env.local"
    ]
}
```

**Note**: `$ROOT_WORKTREE_PATH` is a variable provided by Cursor that references the main repository path, allowing you to copy files from the root worktree to the new worktree.
