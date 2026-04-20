---
description: Ask the Gemini CLI a general question or request a task.
---
# /gemini:ask

Use this command to ask the Gemini CLI a general question or request a task.

## Instructions
When this command is invoked, execute the `gemini` command in the shell with the user's query as an argument and ensure the `--approval-mode auto_edit` flag is used to allow Gemini to perform edits autonomously.

Example:
If the user runs `/gemini:ask how do I optimize this function?`, you should execute:
`gemini --approval-mode auto_edit "how do I optimize this function?"`
