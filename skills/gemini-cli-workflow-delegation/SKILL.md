---
name: gemini-cli-workflow-delegation
description: Delegated tasks to global Antigravity workflows using the gemini CLI. Use this to parallelize work across specialized workflows while maintaining visibility in the Agent Manager.
---

# CLI Workflow Delegation Skill

This skill allows the agent to orchestrate complex tasks by triggering global workflows registered in the Antigravity system using the `gemini` CLI. It ensures that sub-workflows are properly tracked and visible for review in the Agent Manager.

## When to use this skill

- To trigger specialized global workflows (from `~/gemini/antigravity/global_workflows`) via CLI.
- To execute many parallel workflows as part of a larger ADD (Agent-Driven Development) cycle.
- When the execution needs to be monitored and managed via the Antigravity Agent Manager.

## How to use it

### 1. Workflow Identification

The agent must identify the correct workflow name from the global registry (e.g., `/engineer-agent`, `/architect-agent`). These are invoked directly as slash commands within the prompt string.

### 2. Execution Template

Use the `run_command` tool to execute the `gemini` binary.

#### Non-Interactive (Recommended for Orchestration)

Use the `-p` flag for background tasks and `-m` to specify the model. To ensure maximum autonomy during parallel execution, always append `--approval-mode=yolo` to prevent tool execution blocks.

#### Parallel Asynchronous Execution & Staggered Throttling (Avoid Capacity Errors)

To run multiple workflows concurrently with different results, trigger them in **separate, isolated PowerShell instances** so they run in parallel without blocking each other. 

> [!IMPORTANT]
> **Do NOT run multiple task initiations inside a single multi-line shell script or command block.** The Orchestrator agent must trigger each task in **separate, distinct shell interactions (separate `run_command` tool calls)**. 

Because spawning multiple agents simultaneously (bursts) can exhaust the transient **RPM (Requests Per Minute)** or **TPM (Tokens Per Minute)** quotas of the Gemini API due to heavy initial context loading, you must:
1. Trigger the first task using a single `run_command` tool call.
2. **Wait 5 to 10 seconds** before making the next `run_command` tool call for the subsequent task.
3. Spawn each workflow in its own PowerShell window/instance using `Start-Process powershell`.

##### Command for the first task (executed in tool call #1):
```powershell
Start-Process powershell -ArgumentList "-NoProfile -NoExit -Command `\"gemini -p `\"/engineer-agent implement Task 001...`\" --approval-mode=yolo`\""
```

##### Command for the second task (executed in tool call #2, after a 5-10 seconds delay):
```powershell
Start-Process powershell -ArgumentList "-NoProfile -NoExit -Command `\"gemini -p `\"/engineer-agent implement Task 002...`\" --approval-mode=yolo`\""
```

### 3. Orchestration & Centralization (The Conductor Role)

The agent invoking this skill (the current agent in the chat) acts as the **central point** of the operation.

- **Mandatory Synchronization**: You **MUST** monitor the status of the command using `command_status`.
- **Interaction Relay**: If the command output indicates that the subagent is waiting for user input or decision, pass the question along in this chat and use `send_command_input` to send the response to the subagent.
- **Output Capture**: Once the subagent finishes, you must read the final report and use it to update the project state (roadmap T-file, etc.) and inform the user.
- **Visibility**: The Agent Manager groups the sessions automatically via the process tree.

### 4. Windows Background Execution & ConPTY Troubleshooting

On Windows, running the CLI in the background in parallel processes can result in the `AttachConsole failed` error originating from the `node-pty` / ConPTY library.

To troubleshoot or prevent this behavior, **disable the interactive shell** in the global CLI settings (`~/.gemini/settings.json`), which forces a safe fallback to `child_process.spawn`:

```json
{
  "tools": {
    "shell": {
      "enableInteractiveShell": false
    }
  }
}
```

> [!IMPORTANT]
> Only use the `gemini` command. Do not use the `run` subcommand. The name of the workflow (starting with `/`) must be the first term within the prompt quotes.
> Use `--approval-mode=yolo` to ensure subagents operate with full autonomy in parallel executions.
