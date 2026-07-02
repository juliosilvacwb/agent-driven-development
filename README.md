# Agent-Driven Development (ADD)

Agent-Driven Development (ADD) is a framework that evolves traditional software development workflows into a structured pipeline of specialized AI agents. It applies the rigor of Agile and the discipline of TDD to an engineering assembly line where the human acts as the conductor and the final guarantor of quality.

## Core Principle: Documentation as the Single Source of Truth
In ADD, context is preserved in Markdown (`.md`) files. These artifacts serve as the project's living memory, ensuring that both human developers and AI agents operate on the same set of facts, requirements, and technical decisions.

## The ADD Pipeline

The ADD workflow uses specialized agents for each stage of development:

1.  **[PM Agent](./pm-agent/)**: The "Strategist". Transforms business vision into prioritized product ideas through structured brainstorming, market analysis, and strategic prioritization. **Scope: Ideation and opportunity mapping only. Does not write PRDs or technical specs.**
2.  **[Discovery Agent](./discovery-agent/)**: The "Archaeologist". Performs forensics on existing code to establish technical facts.
3.  **[PO Agent](./po-agent/)**: The "Interrogator". Refuses vague requests and converts ideas into detailed PRDs.
4.  **[Architect Agent](./architect-agent/)**: The "Blueprint Maker". Bridges the gap between requirements and code with a technical roadmap. **Scope: Technical specification only. Does not implement code or delegate tasks.**
5.  **[Orchestrator Agent](./orchestrator-agent/)**: The "Conductor". Senior Engineer responsible for adaptive orchestration, parallelization, and task delegation to subagents.
6.  **[Engineer Agent](./engineer-agent/)**: The "Muscle". Executes structured tasks (from T, B, S, or TEST files) following strict TDD. **Scope: Atomic task implementation. Focuses exclusively on the current task without look-ahead or delegation.**
7.  **[Debugger Agent](./debugger-agent/)**: The "Investigator". Proves errors with failing tests before proposing any fix.
8.  **[Security Agent](./security-agent/)**: The "DevSecOps Guardian". Performs SAST/DAST on implemented code and generates actionable vulnerability fix loops.
9.  **[Test Agent](./test-agent/)**: The "Forensics Expert". Analyzes code for coverage gaps and generates precision testing roadmaps. **Scope: Coverage discovery and test specification only.**
10. **[Quality Agent](./quality-agent/)**: The "Gatekeeper". Final reviewer who cross-validates business intent, technical standards, security patches, and test coverage.
11. **[Documentation Agent](./documentation-agent/)**: The "Librarian". Synchronizes the specs, plans, and final implementation.



## Skills

Skills are reusable knowledge packages that extend agent capabilities. They encode architectural patterns, conventions, and strategies that agents apply during their workflow.

| Skill | Description | Primary Consumer |
|-------|-------------|-----------------|
| [hexagonal-parallelism](./skills/hexagonal-parallelism/) | Applies Hexagonal Architecture as an industrial parallelism strategy — maximizing decoupling to enable parallel task execution by AI agents. | Architect Agent |

See the [skills directory](./skills/) for the full catalog.

## How to Use This Project

This repository serves as a template and a reference for implementing Agent-Driven Development in your own projects. Each directory contains:

-   **README.md**: Explaining the agent's role, responsibilities, and behavior.
-   **prompt.md**: The "System Prompt" or "Creation Prompt" to configure an LLM to act as that specific agent.

### Getting Started

1.  **Define the Brain**: Choose a high-reasoning model (e.g., Gemini Pro, Claude Opus) for the PO and Architect roles to ensure depth and clarity.
2.  **Define the Muscle**: Choose a fast, instruction-following model (e.g., Gemini Flash) for the Engineer role to optimize for speed and adherence to the plan.
3.  **Create the Artifacts**: Ensure your project has a `/docs` directory to store the following:
    -   `/docs/product-strategy/` (PS-files)
    -   `/docs/discovery/` (D-files)
    -   `/docs/business-requirements/` (R-files)
    -   `/docs/architecture/` (T-files)
    -   `/docs/quality/` (Q-files: Validation reports and audit trails)
    -   `/docs/security/` (S-files: Vulnerability logs and fixes)
    -   `/docs/tests/` (TEST-files: Coverage gaps and tasks)
    -   `/docs/bugs/` (B-files: Incident and reproduction scripts)

### Invoking Agents

Each agent is triggered by calling their slash command followed by a descriptive prompt detailing the task at hand. 

Here is an example prompt for each agent:

- **PM Agent**:
  ```markdown
  /pm-agent brainstorm feature ideas to increase user engagement in our financial management platform
  ```
- **Discovery Agent**:
  ```markdown
  /discovery-agent locate the authentication logic and document it in D001-auth.md
  ```
- **PO Agent**:
  ```markdown
  /po-agent create a business requirements spec for the subscription payment system
  ```
- **Architect Agent**:
  ```markdown
  /architect-agent create the technical implementation plan for R001-subscriptions.md
  ```
- **Orchestrator Agent**:
  ```markdown
  /orchestrator-agent execute the roadmap tasks listed in T001-subscriptions.md
  ```
- **Engineer Agent**:
  ```markdown
  /engineer-agent implement task T001 in T001-subscriptions.md
  ```
- **Debugger Agent**:
  ```markdown
  /debugger-agent a user told me that receive an error message when login in the app, the error is "null pointer exception", the error occur in the login controller, the user login page is at /login
  ```
- **Security Agent**:
  ```markdown
  /security-agent analize the implementation of Task 001 in T001-subscriptions.md and search for any security vulnerabilities
  ```
- **Test Agent**:
  ```markdown
  /test-agent analize the implementation of Task 001 in T001-subscriptions.md and check test coverage
  ```
- **Quality Agent**:
  ```markdown
  /quality-agent review the implementation of T001-subscriptions.md
  ```
- **Documentation Agent**:
  ```markdown
  /documentation-agent synchronize API docs and diagrams with the T001-subscriptions.md implementation
  ```

### Status Lifecycle & Immutability

To prevent "technical amnesia" and context drift, ADD follows a strict status lifecycle for every task, requirement, and test:
-   **Pending `[ ]`**: Work not started.
-   **Done `[x]`**: Work completed by an agent (Engineer, PO, etc.) and ready for review.
-   **APPROVED `[APPROVED]` / `[COMPLETED]`**: Finalized by the **Quality Agent** (Approved) or the **Documentation Agent** (Completed).

**The Gold Rule of Immutability**: Any item marked as `[APPROVED]` or `[COMPLETED]` is considered final and immutable. Agents are strictly forbidden from re-evaluating or re-modifying finalized items, ensuring a stable foundation for subsequent tasks.

### Separation of Concerns & Orchestration
To maintain high reliability and prevent context drift, ADD enforces a strict separation between **specification** (Architect, PO, Test Agent) and **execution** (Engineer, Debugger, Security Agent). 

- **Specialized agents** are forbidden from calling subagents or looking beyond their immediate atomic scope.
- **Orchestration** is handled by the **Orchestrator Agent**, which manages the end-to-end execution of roadmaps through parallel subagent delegation.
- **Human Oversight**: The developer remains the final "Circuit Breaker," validating the Orchestrator's progress and results.

### The Human Role: The Circuit Breaker
The ADD framework is NOT an autopilot. It is power steering for developers. You must validate the output of each stage. If an agent loops, oscillates, or over-engineers, you intervene. You decide when an agent's cycle is complete.

---

> *"The secret to scaling with AI is not the size of the prompt, but the management of application state through persistent artifacts."*
