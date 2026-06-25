---
name: agy-cli-workflow-delegation
description: Delegated tasks to global Antigravity workflows using the agy CLI. Use this to parallelize work across specialized workflows while maintaining visibility in the Agent Manager.
---

# AGY CLI Workflow Delegation Skill

This skill allows the agent to orchestrate complex tasks by triggering global workflows registered in the Antigravity system using the `agy` CLI. It ensures that sub-workflows are properly tracked and visible for review in the Agent Manager.

## When to use this skill

- To trigger specialized global workflows (from `~/.gemini/config/global_workflows`) via the `agy` CLI.
- To execute many parallel workflows as part of a larger ADD (Agent-Driven Development) cycle.
- When the execution needs to be monitored and managed via the Antigravity Agent Manager.

## How to use it

### 1. Workflow Identification

The agent must identify the correct workflow name from the global registry (e.g., `/engineer-agent`, `/architect-agent`). These are invoked directly as slash commands within the prompt string.

### 2. Execution Template

Use the `run_command` tool to execute the `agy` binary.

#### Non-Interactive (Recommended for Orchestration)

Use the `-p` (or `--print`/`--prompt`) flag to run a single prompt non-interactively, and `--model` to specify the model if needed. To ensure maximum autonomy during parallel execution, always append `--dangerously-skip-permissions` to prevent tool execution permission blocks.

#### Parallel Asynchronous Execution & Staggered Throttling (Avoid Capacity Errors)

To run multiple workflows concurrently with different results, trigger them in **separate, isolated commands** so they run in parallel without blocking each other.

> [!IMPORTANT]
> **Do NOT run multiple task initiations inside a single multi-line shell script or command block.** The Orchestrator agent must trigger each task in **separate, distinct shell interactions (separate `run_command` tool calls)**. 

Because spawning multiple agents simultaneously (bursts) can exhaust the transient **RPM (Requests Per Minute)** or **TPM (Tokens Per Minute)** quotas of the Gemini API due to heavy initial context loading, you must:
1. Trigger the first task using a single `run_command` tool call.
2. **Wait 5 to 10 seconds** before making the next `run_command` tool call for the subsequent task.

##### Command for the first task (executed in tool call #1):
```powershell
agy -p "/engineer-agent implement Task 001..." --dangerously-skip-permissions
```

##### Command for the second task (executed in tool call #2, after a 5-10 seconds delay):
```powershell
agy -p "/engineer-agent implement Task 002..." --dangerously-skip-permissions
```

### 3. Orchestration & Centralization (The Conductor Role)

The agent invoking this skill (the current agent in the chat) acts as the **central point** of the operation.

- **Mandatory Synchronization**: You **MUST** monitor the status of the command using the task management tools (e.g. `manage_task` or equivalent command monitoring).
- **Interaction Relay**: If the command output indicates that the subagent is waiting for user input or decision, pass the question along in this chat and use the input relay (e.g. `manage_task send_input`) to send the response to the subagent.
- **Output Capture**: Once the subagent finishes, you must read the final report and use it to update the project state (roadmap T-file, etc.) and inform the user.
- **Visibility**: The Agent Manager groups the sessions automatically via the process tree.

### 4. Windows Background Execution & ConPTY Troubleshooting

On Windows, running the CLI in the background in parallel processes can result in the `AttachConsole failed` error or cause the process to hang indefinitely due to the `node-pty` / ConPTY library trying to allocate a terminal.

To prevent this behavior, you **MUST** ensure the interactive shell is disabled in the CLI settings file. 

#### Mandatory Validation Before Triggering Subagents:
1. **Locate the Settings File**: Check if the CLI settings file exists at `~/.gemini/antigravity-cli/settings.json` (typically `C:\Users\<username>\.gemini\antigravity-cli\settings.json`).
2. **Verify Configuration**: Read the file and ensure it has the following configuration:
   ```json
   {
     "tools": {
       "shell": {
         "enableInteractiveShell": false
       }
     }
   }
   ```
3. **Auto-Configure**: If `enableInteractiveShell` is `true`, missing, or the file does not exist:
   - Ask the user's permission to configure it.
   - Once approved, modify or create the settings file to set `"enableInteractiveShell": false` under `"tools" -> "shell"` **before** invoking any background `agy` commands.

> [!IMPORTANT]
> Only use the `agy` command. The name of the workflow (starting with `/`) must be the first term within the prompt quotes.
> Use `--dangerously-skip-permissions` to ensure subagents operate with full autonomy in parallel executions.
