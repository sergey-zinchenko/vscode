# Pull requests (fork workflow)

Canonical integration repo for this project: **`sergey-zinchenko/vscode`**. Upstream Microsoft repo: **`microsoft/vscode`** — never use it as a PR target for fork work.

## Remote layout

| Clone type | Typical `origin` | Typical `upstream` | Where the PR opens |
| --- | --- | --- | --- |
| Integration fork (maintainers) | `sergey-zinchenko/vscode` | `microsoft/vscode` (sync only) | `sergey-zinchenko/vscode` → `main` |
| Contributor fork | `your-user/vscode` | `sergey-zinchenko/vscode` | `sergey-zinchenko/vscode` → `main`, head `your-user:branch` |
| Nested fork (fork of a fork) | `your-user/vscode` | `other-user/vscode` or `sergey-zinchenko/vscode` | Parent repo from `upstream` (if not `microsoft/vscode`), head `your-user:branch` |
| Personal fork, no `upstream` remote | `your-user/vscode` | — | Default to `sergey-zinchenko/vscode`, head `your-user:branch` |

Always **push** to `origin`. Never push feature branches to `microsoft/vscode`.

## Resolve PR target (agents and automation)

1. Parse `git remote get-url origin` → **push repo** (where the branch is published).
2. Parse `git remote get-url upstream` if present → **parent repo**.
3. Choose **PR base repo** (`--repo` / API `owner`+`repo`):
   - **Never** `microsoft/vscode`.
   - If `upstream` exists and is **not** `microsoft/vscode` → PR base = `upstream`.
   - Else if `origin` is `sergey-zinchenko/vscode` → PR base = `sergey-zinchenko/vscode`.
   - Else (personal fork without a useful `upstream`) → PR base = `sergey-zinchenko/vscode`.
4. Choose **head**:
   - Same repo as PR base → head = current branch name (e.g. `feat/foo`).
   - Cross-repo → head = `{origin-owner}:{branch}` (e.g. `your-user:feat/foo`).
5. Base branch is usually **`main`** unless the user specifies another base.
6. After creation, verify the PR URL is `https://github.com/{pr-base-owner}/{repo}/pull/...` and **not** `microsoft/vscode`.

## Examples

**Maintainer (origin = integration fork):**

```bash
git push -u origin HEAD
gh pr create --repo sergey-zinchenko/vscode --base main --head "$(git branch --show-current)"
```

**Contributor (origin = your fork, upstream = integration fork):**

```bash
git push -u origin HEAD
gh pr create --repo sergey-zinchenko/vscode --base main --head "$(gh api user -q .login):$(git branch --show-current)"
```

**Nested fork (origin = your fork, upstream = another fork):**

```bash
git push -u origin HEAD
# PR base = owner/repo parsed from `git remote get-url upstream`
gh pr create --repo OTHER-USER/vscode --base main --head "$(gh api user -q .login):$(git branch --show-current)"
```

## Recommended git remotes

Contributors should configure:

```bash
git remote add upstream https://github.com/sergey-zinchenko/vscode.git   # if missing
# Do NOT use microsoft/vscode as upstream when opening PRs for fork features.
```

Maintainers syncing Microsoft releases may keep `upstream` → `microsoft/vscode` for merges; PRs for fork work still target `sergey-zinchenko/vscode` (see step 3 above).
