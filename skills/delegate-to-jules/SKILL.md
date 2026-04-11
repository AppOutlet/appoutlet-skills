---
name: delegate-to-jules
description: When the user wants to delegate a plan, task, or implementation to Jules (the remote coding agent), run this plan remotely, or let Jules do the work while they do something else.
---
# Delegate to Jules

Use this skill when the user wants to hand off a plan or task to Jules, Google's autonomous AI coding agent.

## Procedure

1.  **Mandatory CLI Verification:** You MUST verify the `jules` CLI is installed BEFORE any other action. Run `jules version` quietly. If it fails, stop and tell the user to run `npm install -g @google/jules`. **Do not skip this step.**
2.  **Locate the Plan:** Search the repository for plan files — look for Markdown or text files in common planning directories (e.g., any `plans/` folder, agent workspace directories, or similar). Read the file to extract its full content — do NOT use the file path as the prompt, since plan files are not committed to version control and Jules cannot access them by path.
3.  **Handle Missing Plan:** If you cannot find a relevant plan file:
    *   Do not guess or proceed autonomously. Ask the user to choose — use whatever mechanism your platform provides (an interactive prompt, a choice widget, a plain question, etc.):
        *   Option A: Use the plan from the current conversation context
        *   Option B: Abort the delegation
    *   If they abort, stop. If they confirm, extract the plan from the chat history (or any text they supply) and use that as the plan content.
4.  **Delegate:**
    *   Pass the plan content to Jules by reading from the file using shell substitution — never embed raw text or pass a bare file path as the session value.
    *   If the plan is in a file, use the appropriate command for the platform:
        *   macOS / Linux: `jules remote new --session "$(cat path/to/plan.md)"`
        *   Windows (PowerShell): `jules remote new --session (Get-Content path\to\plan.md -Raw)`
    *   If the plan came from chat history or user-provided text (no file), write it to a temporary file first, then use the same shell substitution pattern above.
5.  **Mandatory Wrap Up:** Once the command succeeds, you MUST explicitly inform the user that the plan was handed over and state: **"I am now leaving plan mode so you can continue with other work."** This exact phrase is required to signal the end of the delegation process.