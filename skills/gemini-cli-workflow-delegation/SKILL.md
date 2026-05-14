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

Use the `-p` flag ONLY for background tasks where NO interaction or monitoring is required.

```powershell
gemini -p "/engineer-agent implement Task 001 - [Domain-Model]: Create User entity"
```

### 3. Orchestration & Centralization (The Conductor Role)

O agente que invoca esta skill (o agente atual no chat) atua como o **ponto centralizador** da operação.

- **Sincronização Obrigatória**: Você **DEVE** monitorar o status do comando usando `command_status`.
- **Relay de Interação**: Se a saída do comando indicar que o subagente está esperando por input ou decisão do usuário, repasse a pergunta neste chat e use `send_command_input` para enviar a resposta ao subagente.
- **Captura de Saída**: Uma vez que o subagente finalize, você deve ler o relatório final e usá-lo para atualizar o estado do projeto (roadmap T-file, etc.) e informar o usuário.
- **Visibilidade**: O Agent Manager agrupa as sessões automaticamente através da árvore de processos.

> [!IMPORTANT]
> Apenas use o comando `gemini`. Não utilize o subcomando `run`. O nome do workflow (iniciando com `/`) deve ser o primeiro termo dentro das aspas do prompt.