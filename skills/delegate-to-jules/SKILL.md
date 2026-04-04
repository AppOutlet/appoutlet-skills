---
name: delegate-to-jules
description: When the user wants to delegate a plan, task, or implementation to Jules (the remote coding agent), run this plan remotely, or let Jules do the work while they do something else.
---
# Delegate to Jules

Use this skill when the user wants to hand off a plan or task to Jules, Google's autonomous AI coding agent.

## Procedure

1.  **Mandatory CLI Verification:** You MUST verify the `jules` CLI is installed BEFORE any other action. Run `jules version` quietly. If it fails, stop and tell the user to run `npm install -g @google/jules`. **Do not skip this step.**
2.  **Locate the Plan:** Search for the relevant plan inside `.gemini/plans/`. Look for Markdown files or other text files that contain the active plan.
3.  **Handle Missing Plan:** If you cannot find a relevant plan file in `.gemini/plans/`:
    *   Do not guess. You MUST confirm with the user before using the chat history context as the plan.
    *   Use the `ask_user` tool with a `choice` question:
        *   Option 1: Label: "Use current context", Description: "Extract the plan from chat history"
        *   Option 2: Label: "Abort", Description: "Cancel the delegation"
    *   If they abort, stop. If they provide custom text, use that as the plan.
4.  **Delegate:**
    *   Extract the plan content (from the file, chat history, or user text).
    *   Execute the plan: `jules remote new --session "<plan_text_or_summary>"`.
    *   Ensure the plan text is safely escaped for the bash command.
5.  **Mandatory Wrap Up:** Once the command succeeds, you MUST explicitly inform the user that the plan was handed over and state: **"I am now leaving plan mode so you can continue with other work."** This exact phrase is required to signal the end of the delegation process.