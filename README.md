# Agent Skills Collection

This repository is a collection of skills and references to skills that are highly useful for AI agents.

It functions as a plugin system that can be loaded into major AI agent providers, allowing your AI coding assistant to learn new behaviors and workflows natively.

## How it works

This project provides structured instructions ("skills") that teach AI agents how to perform specific complex tasks. The plugin system is designed to be universally compatible with almost any major AI agent provider.

It contains configuration files (`CLAUDE.md`, `GEMINI.md`, `AGENTS.md`, etc.) that automatically instruct your agent to read and load the skills from the `skills/` directory when they are relevant.

## Available Skills

* **Git Codebase Health Report**: Analyzes one or more git repositories using their commit history to assess codebase health, risk, and team dynamics — all before reading any source code.

## Compatibility

This repository is compatible with major AI agents. It uses specific fallback mechanisms and configuration files so it works even on platforms that don't have a formalized plugin registry.

* **Claude Code / Cursor**: Uses `.claude-plugin`, `.cursor-plugin`, and `CLAUDE.md`/`.cursorrules`
* **Gemini**: Compatible via `GEMINI.md` context files
* **OpenCode / Codex**: Compatible via `.opencode/` and `.codex/` configurations
* **Antigravity / Generic**: Compatible via `ANTIGRAVITY.md` and `AGENTS.md`

Simply by including this repository's files in your workspace, or by loading it as a plugin/submodule, your AI assistant will gain access to these powerful new capabilities.
