# Gemini Plugin: Contributor & Subagent Reference

This guide provides architectural context and operational guidelines for AI agents (including Claude Code, Gemini CLI, and specialized subagents) working within this repository.

## Repository Overview

This repository contains a **Claude Code plugin** that integrates Gemini capabilities via the local `gemini` CLI.

- **Marketplace Manifest**: `.claude-plugin/marketplace.json` (Defines the registry)
- **Plugin Manifest**: `plugins/gemini/.claude-plugin/plugin.json` (Defines commands and agents)
- **Plugin Implementation**: `plugins/gemini/`

## Operational Guidelines

### 1. Release Management
- **Tool**: [release-please](https://github.com/googleapis/release-please)
- **Mechanism**: Managed via `release-please-config.json` and `.release-please-manifest.json`.
- **Version Sync**: `release-please` is configured to automatically sync the version from `package.json` into:
  - `.claude-plugin/marketplace.json` (`$.metadata.version`)
  - `plugins/gemini/.claude-plugin/plugin.json` (`$.version`)
- **Workflow**: Agents should NOT manually bump versions. Always use **Conventional Commits** (e.g., `feat:`, `fix:`) to trigger automated Release PRs.

### 2. Git & Branching
- **Branch Naming**: Follow conventional commit patterns for branches (e.g., `feat/feature-name`, `fix/bug-fix`, `docs/update-readme`).
- **Standard Flow**: Always work on feature/fix branches and open PRs to `main`.

### 3. Manifest Schemas
- **Strict Validation**: Claude Code manifest files (`plugin.json`, `marketplace.json`) have strict schema requirements:
  - `author` and `owner` must be **objects** with a `name` field.
  - Paths in `marketplace.json` are relative to the repository root.
  - Paths in `plugin.json` are relative to the plugin directory.

## Subagent Definitions (Internal)

### `@gemini-rescue`
- **Definition**: `plugins/gemini/agents/gemini-rescue.md`
- **Role**: Fresh-perspective debugging by delegating to local Gemini CLI.
- **Protocol**: Operates via `run_shell_command("gemini '...'")`.

## Maintenance Tasks
- Ensure any new commands added to `plugins/gemini/commands/` are also documented in `README.md`.
- Ensure new agents added to `plugins/gemini/agents/` are reflected in the `plugin.json` manifest if automatic discovery is insufficient.
