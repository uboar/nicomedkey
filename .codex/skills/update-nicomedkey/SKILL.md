---
name: update-nicomedkey
description: Update the nicomedkey repository by checking the latest GitHub release from misskey-dev/misskey, merging that release commit into the local branch, resolving conflicts with preference for local nicomedkey changes, updating the root package.json version to the Misskey release version plus -nicomedkey, and documenting how container publishing should run from GitHub Actions on pushes to main.
Use when Codex is asked to sync nicomedkey with upstream Misskey releases or prepare the repository for release automation after upstream updates.
---

# Update nicomedkey

## Overview

Follow this workflow to update this repository against the latest upstream Misskey release and keep the repository aligned with GitHub Actions based container publishing.

Work from the repository root on the local branch unless the user explicitly asks for a different branch.

## Workflow

### 1. Ensure remotes are configured

```bash
git remote get-url origin
git remote get-url upstream || git remote add upstream https://github.com/misskey-dev/misskey.git
```

### 2. Fetch upstream tags and branches

```bash
git fetch upstream --tags
```

### 3. Resolve the latest release commit from misskey-dev/misskey

Use `gh release view` or the GitHub API to identify the latest release tag, then map the tag to a commit and merge it:

```bash
git merge <release-commit>
```

If Git reports no changes because the release commit is already contained, continue with version checks only if the user still wants the repository state refreshed.

### 4. Resolve conflicts with nicomedkey precedence

When conflicts happen, keep nicomedkey customizations unless the user explicitly requests upstream behavior.

### 5. Update root package version

Set the root `package.json` version to:

`<misskey-version>-nicomedkey`

Example:

`2026.4.0-nicomedkey`

Only the root `package.json` needs this version change unless the user asks for broader version alignment.

### 6. Document GitHub Actions based container publishing

Do not treat local `docker build` as part of the default update workflow.

When the user wants container publishing, explain that it should be handled by a GitHub Actions workflow triggered by pushes to `main`, then published to Docker Hub. Keep the explanation concrete:

- Create or update a workflow under `.github/workflows/docker.yml`.
- Change the trigger to:

```yaml
on:
  push:
    branches:
      - main
  workflow_dispatch:
```

### 7. Report result

Summarize:

- Latest upstream release/tag used.
- Merge result (fast-forward, merge commit, or already up to date).
- Any conflicts and how they were resolved.
- Final `package.json` version.
- Whether the GitHub Actions workflow is aligned for publish-on-main.
