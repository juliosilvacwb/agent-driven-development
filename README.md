# Agent-Driven Development (ADD)

Agent-Driven Development (ADD) is a framework that evolves traditional software development workflows into a structured pipeline of specialized AI agents. It applies the rigor of Agile and the discipline of TDD to an engineering assembly line where the human acts as the conductor and the final guarantor of quality.

## Core Principle: Documentation as the Single Source of Truth
In ADD, context is preserved in Markdown (`.md`) files. These artifacts serve as the project's living memory, ensuring that both human developers and AI agents operate on the same set of facts, requirements, and technical decisions.

## The ADD Pipeline

The ADD workflow uses specialized agents for each stage of development:

1.  **[Discovery Agent](./discovery-agent/)**: The "Archaeologist". Performs forensics on existing code to establish technical facts.
2.  **[PO Agent](./po-agent/)**: The "Interrogator". Refuses vague requests and converts ideas into detailed PRDs.
3.  **[Architect Agent](./architect-agent/)**: The "Blueprint Maker". Bridges the gap between requirements and code with a technical roadmap. **Scope: Technical specification only. Does not implement code or delegate tasks.**
4.  **[Orchestrator Agent](./orchestrator-agent/)**: The "Conductor". Senior Engineer responsible for adaptive orchestration, parallelization, and task delegation to subagents.
5.  **[Engineer Agent](./engineer-agent/)**: The "Muscle". Executes structured tasks (from T, B, S, or TEST files) following strict TDD. **Scope: Atomic task implementation. Focuses exclusively on the current task without look-ahead or delegation.**
6.  **[Debugger Agent](./debugger-agent/)**: The "Investigator". Proves errors with failing tests before proposing any fix.
7.  **[Security Agent](./security-agent/)**: The "DevSecOps Guardian". Performs SAST/DAST on implemented code and generates actionable vulnerability fix loops.
8.  **[Test Agent](./test-agent/)**: The "Forensics Expert". Analyzes code for coverage gaps and generates precision testing roadmaps. **Scope: Coverage discovery and test specification only.**
9.  **[Quality Agent](./quality-agent/)**: The "Gatekeeper". Final reviewer who cross-validates business intent, technical standards, security patches, and test coverage.
10. **[Documentation Agent](./documentation-agent/)**: The "Librarian". Synchronizes the specs, plans, and final implementation.



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
    -   `/docs/discovery/` (D-files)
    -   `/docs/business-requirements/` (R-files)
    -   `/docs/architecture/` (T-files)
    -   `/docs/quality/` (Q-files: Validation reports and audit trails)
    -   `/docs/security/` (S-files: Vulnerability logs and fixes)
    -   `/docs/tests/` (TEST-files: Coverage gaps and tasks)
    -   `/docs/bugs/` (B-files: Incident and reproduction scripts)

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
