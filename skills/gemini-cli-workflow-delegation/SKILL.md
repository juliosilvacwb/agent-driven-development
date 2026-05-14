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

#### A. Non-Interactive (Standard Delegation)
Use the `-p` flag for tasks where the agent should execute a specific mission and finish.
```powershell
gemini -p "/engineer-agent implement Task 001 - [Domain-Model]: Create User entity"
```

### 3. Orchestration & Centralization (The Conductor Role)
O agente que invoca esta skill (o agente atual no chat) atua como o **ponto centralizador** da operação.
- **Relay de Interação**: Qualquer dúvida, necessidade de input humano ou decisão de gate gerada pelo subagente será repassada por este chat principal.
- **Visibilidade**: Embora os subagentes rodem em processos separados, o agente atual é responsável por reportar o progresso geral e consolidar os resultados no contexto da conversa atual.
- **Sincronização**: O Agent Manager agrupa as sessões automaticamente através da árvore de processos, mantendo a hierarquia de execução visível para o usuário.

> [!IMPORTANT]
> Apenas use o comando `gemini`. Não utilize o subcomando `run`. O nome do workflow (iniciando com `/`) deve ser o primeiro termo dentro das aspas do prompt.