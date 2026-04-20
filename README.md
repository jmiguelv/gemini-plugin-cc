# Gemini Plugin for Claude Code (`gemini-plugin-cc`)

Integrate Gemini's capabilities directly into your Claude Code sessions. This plugin delegates tasks to your local `gemini` CLI, allowing you to leverage Gemini for code reviews, complex debugging, and general queries without leaving Claude.

## Features

- **`/gemini:review`**: Performs a read-only code review of your current uncommitted changes using Gemini.
- **`/gemini:ask <query>`**: Asks Gemini a specific question or requests a task.
- **`gemini-rescue` Agent**: A specialized subagent that Claude can autonomously invoke (or you can delegate to) when stuck on a difficult bug or architectural decision.

## Requirements

- **Claude Code**: Version 0.0.1 or later.
- **Gemini CLI**: Must be installed and configured in your shell's `PATH`.

## Installation

### 1. Add the Marketplace
Add the GitHub repository as a marketplace in Claude Code:

```bash
claude plugin marketplace add jmiguelv/gemini-plugin-cc
```

### 2. Install the Plugin
Install the `gemini` plugin from the marketplace:

```bash
claude plugin install gemini@gemini-plugins --scope user
```

## Usage

### Commands

Within a Claude Code session, you can use the following slash commands:

- `/gemini:review` - "Gemini, what do you think of these changes?"
- `/gemini:ask "How should I structure this new module?"` - Get a second opinion from Gemini.

### Delegation

If Claude is struggling with a task, you can explicitly delegate it to the Gemini rescue agent:

> "I'm stuck on this race condition. @gemini-rescue, can you take a look?"

## How it Works

This plugin is a lightweight wrapper around the `gemini` CLI. It uses Claude's `run_shell_command` capability to execute `gemini` with specific prompts, passing back the results to the Claude session. This ensures that Gemini has access to the same file context and environment as Claude.
