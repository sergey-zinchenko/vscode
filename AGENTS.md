# VS Code Agents Instructions

This file provides instructions for AI coding agents working with the VS Code codebase.

**Fork notice:** This is [sergey-zinchenko/vscode](https://github.com/sergey-zinchenko/vscode), not vanilla microsoft/vscode. Read [FORK.md](FORK.md) before making changes. Key fork areas:

- **DIAL provider:** `extensions/dial-chat-model-provider/` — bundled language-model chat provider for DIAL Core
- **BYOK pipeline:** `src/vs/workbench/contrib/chat/` (e.g. `hasByokModelsContribution.ts`, `embeddingModelContribution.ts`) and `extensions/copilot/src/platform/workspaceChunkSearch/`, `extensions/copilot/src/platform/endpoint/`

For detailed project overview, architecture, coding guidelines, and validation steps, see the [Copilot Instructions](.github/copilot-instructions.md).
