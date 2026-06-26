---
name: create-draft-pr
description: Create a draft pull request for the current session. Use when the user wants to open a draft PR with the session's changes.
---

> **Fork notice:** This is [sergey-zinchenko/vscode](https://github.com/sergey-zinchenko/vscode), not vanilla [microsoft/vscode](https://github.com/microsoft/vscode). Read [FORK.md](../../../../../FORK.md) before making changes. Key fork areas: DIAL (`extensions/dial-chat-model-provider/`), BYOK (`src/vs/workbench/contrib/chat/`, `extensions/copilot/`).

<!-- Customize this skill and select save to override its behavior. Delete that copy to restore the built-in behavior. -->

# Create Draft Pull Request

**Target repo:** `sergey-zinchenko/vscode` (base: `main`). **Never** create a PR in `microsoft/vscode`.

1. Run the compile and hygiene tasks (fixing any errors)
2. If there are any uncommitted changes, use the `/commit` skill to commit them
3. Review all changes in the current session
4. Push the branch to `origin` (must be `sergey-zinchenko/vscode`, not `upstream`)
5. Write a clear, concise PR title with a short area prefix (e.g. "sessions: …", "editor: …")
6. Write a description covering what changed, why, and anything reviewers should know
7. Create the draft pull request with an explicit repo:
   - **GitHub MCP:** `owner=sergey-zinchenko`, `repo=vscode`, `base=main`, `draft=true`
   - **`gh` CLI:** `gh pr create --repo sergey-zinchenko/vscode --base main --draft ...`
8. Verify the returned URL is `https://github.com/sergey-zinchenko/vscode/pull/...`
