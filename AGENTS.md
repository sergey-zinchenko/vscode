# VS Code Agents Instructions

This file provides instructions for AI coding agents working with the VS Code codebase.

**Fork notice:** This is [sergey-zinchenko/vscode](https://github.com/sergey-zinchenko/vscode), not vanilla [microsoft/vscode](https://github.com/microsoft/vscode). Read [FORK.md](FORK.md) before making changes. Key fork areas: DIAL (`extensions/dial-chat-model-provider/`), BYOK (`src/vs/workbench/contrib/chat/`, `extensions/copilot/`).

- **DIAL provider:** `extensions/dial-chat-model-provider/` — bundled language-model chat provider for DIAL Core
- **BYOK pipeline:** `src/vs/workbench/contrib/chat/` (e.g. `hasByokModelsContribution.ts`, `embeddingModelContribution.ts`) and `extensions/copilot/src/platform/workspaceChunkSearch/`, `extensions/copilot/src/platform/endpoint/`

For detailed project overview, architecture, coding guidelines, and validation steps, see the [Copilot Instructions](.github/copilot-instructions.md).

## Pull requests (fork only)

**Never open pull requests in [microsoft/vscode](https://github.com/microsoft/vscode).**

This repo is an integration fork; others may fork it again. Before creating a PR:

1. **Push** to `origin` (your write remote — may be `your-user/vscode`, not only `sergey-zinchenko/vscode`).
2. **Resolve the PR base repo** from git remotes — do not hardcode your login:
   - If `upstream` exists and is **not** `microsoft/vscode` → open the PR in **`upstream`**.
   - Else if `origin` is `sergey-zinchenko/vscode` → open the PR there.
   - Else (personal fork, no `upstream`) → open the PR in **`sergey-zinchenko/vscode`** with head `your-user:branch`.
3. Use base branch **`main`** unless the user says otherwise.
4. Verify the PR URL is **not** `github.com/microsoft/vscode/pull/...`.

Full algorithm, tables, and examples: [.github/instructions/pull-requests.instructions.md](.github/instructions/pull-requests.instructions.md).

```bash
git push -u origin HEAD
# Same repo as origin → --head <branch>
# Cross-fork → --head <origin-owner>:<branch>
gh pr create --repo <pr-base-owner>/vscode --base main --head <head> --title "..." --body "..."
```

GitHub MCP / API: set `owner` and `repo` from the resolved **PR base**, not from `package.json` alone.

## Production installer (fork)

To build an unsigned, size-optimized Windows x64 installer with DIAL + BYOK:

- **Full guide:** [build/custom/PRODUCTION-BUILD.md](build/custom/PRODUCTION-BUILD.md)
- **Agent quick reference:** [.github/instructions/production-build.instructions.md](.github/instructions/production-build.instructions.md)

Key steps: `npm run compile-dial` → extension gulp tasks → esbuild bundle → `$env:CI='true'` → `vscode-win32-x64-min-ci` → Inno Setup tasks.
