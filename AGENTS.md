# Gemini Plugin Agents Reference

This plugin provides specialized agents (subagents) that can be invoked within a Claude Code session to leverage Gemini's capabilities for complex tasks.

## Available Agents

### `@gemini-rescue`

The Rescue subagent is designed to act as a "fresh perspective" when the primary Claude agent is stuck, hitting a wall with a bug, or facing a complex architectural decision.

- **Primary Goal**: Leverage the local `gemini` CLI to investigate and solve problems.
- **When to Use**:
  - Claude is stuck on a difficult bug.
  - You need an alternative architectural approach.
  - You want to pressure-test a solution using a different model context.
- **Capabilities**:
  - Analyzes the current session context.
  - Formulates and executes queries to the Gemini CLI.
  - Iterates on findings to propose or apply fixes.

## How to Invoke

In a Claude Code session, you can invoke agents using the `@` symbol or by delegating a task:

- **Explicit Mention**: `@gemini-rescue Can you look at the race condition in src/auth.ts?`
- **Delegation**: `delegate to gemini-rescue to investigate why the tests are failing.`

## Technical Details

- **Definition File**: `plugins/gemini/agents/gemini-rescue.md`
- **Model Configuration**: Defaults to Gemini via the local CLI delegation.
- **Context Sharing**: The subagent operates on the same local workspace and file system as the primary Claude session.
