# Gemini CLI Prompt Collection

This repository tracks the evolution of Google's Gemini CLI system prompts and tool definitions across versions.

## Overview

The Gemini CLI is an open-source AI coding assistant from Google. This repository extracts system prompts from each tagged version in the [gemini-cli repository](https://github.com/google-gemini/gemini-cli) and commits them to track changes over time.

## Collection Method

Since Gemini CLI's prompts are embedded in TypeScript code rather than separate markdown files, we extract the source files directly:

1. Checkout each `v0.*` tag in the Gemini CLI repo
2. Copy prompt source files:
   - `packages/core/src/core/prompts.ts` → `prompts/prompts.ts` (system prompt implementation)
   - `packages/core/src/tools/tool-registry.ts` → `tools/tool-registry.ts` (tool definitions)
3. Commit to this repository

This approach preserves the full implementation including conditional logic and dynamic prompt generation.

## Repository Structure

```
gemini-prompts/
├── prompts/
│   └── prompts.ts           # System prompt implementation
├── tools/
│   └── tool-registry.ts     # Tool registry implementation
├── collect.ts               # Collection script
└── README.md
```

## Usage

### Initial Setup

```bash
npm install
```

### Collect All Versions

```bash
npm start
```

### Collect Starting From Specific Version

```bash
npm run start:from=v0.1.0
```

### Limit Collection for Testing

```bash
npm start -- --limit=10
```

## Viewing Changes

View the evolution of prompts using git history:

```bash
# See all versions
git log --oneline

# View changes in a specific file
git log -p prompts/prompts.ts

# Compare two versions
git diff v0.1.0 v0.1.10 prompts/prompts.ts
```

## Requirements

- Node.js 20+
- Access to the Gemini CLI repository at `/Users/pavel/src/gemini-cli`

## Related

- [Claude Code Prompts](https://github.com/p0/claude-code-prompts) - Similar collection for Claude Code CLI
- [Codex Prompts](https://github.com/p0/codex-prompts) - Similar collection for OpenAI Codex CLI
