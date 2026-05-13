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
The agent must identify the correct workflow name from the global registry (e.g., `/engineer-agent`, `/architect-agent`). These are invoked directly as slash commands within the prompt.

### 2. Context & Tracking (Agent Manager Visibility)
The Antigravity system automatically links sub-sessions to the current task using environment variables. You do NOT need to pass these as CLI flags. The following variables are used internally by the `gemini` CLI when running in an Antigravity workspace:

- `ANTIGRAVITY_WORKSPACE_ID`: Identifies the current project.
- `CURRENT_TASK_ID`: Sets the parentage for the sub-task.

### 3. Execution Template
Use the `run_command` tool to execute the `gemini` binary. Use the `-p` (prompt) flag for non-interactive execution (standard for delegation).

```powershell
# Exemplo: Delegando uma tarefa para o Engineer Agent
gemini -p "/engineer-agent implement Task 001 - [Domain-Model]: Create User entity from docs/architecture/T001-user-api.md"
```

### 4. Interactive Mode
If the task requires user interaction or manual approval steps within the sub-session, use the `-i` flag:

```powershell
# Exemplo: Iniciando um workflow em modo interativo
gemini -i "/architect-agent design technical roadmap for R002-checkout.md"
```

> [!IMPORTANT]
> The command is `gemini`, NOT `gemini-cli`. Do not use `run` as a subcommand; pass the workflow name (starting with `/`) directly inside the prompt string.