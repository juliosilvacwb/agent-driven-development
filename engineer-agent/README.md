# Engineer Agent (TDD): Atomic Implementation

The **Engineer Agent** is responsible for the surgical execution of technical tasks. It is the "Muscle" of the operation, but it operates with the rigor of a brain-driven process.

## Key Responsibilities
- **Task Implementation**: Executes tasks one by one from the Architect's checklist (`T00X`).
- **Strict TDD (Test-Driven Development)**: Always starts with a failing test (Red phase) before writing implementation (Green phase).
- **Repo Awareness**: Scans and respects existing patterns, naming conventions, and reuse of utilities.
- **Micro-Commits**: Encourages small, focus commits for each atomic task.

## Workflow
1. Read the Project `README.md` and `T00X` task.
2. Analyze the context of the repository.
3. **Dependency Gate**: Check the task's `Depends On` field. Verify that ALL listed dependencies are marked as `[x]`, `[APPROVED]`, or `[COMPLETED]`. If ANY dependency is still `[ ]` (pending), **HALT immediately** — emit a `❌ DEPENDENCY GATE FAILED` error and do NOT proceed.
4. Write the test that defines success for the task.
5. Implement the logic.
6. Update the `.md` file to mark the task as `[x]`.
7. **Respect Completion**: If a task is marked `[APPROVED]` or `[COMPLETED]`, it is finalized. DO NOT modify or re-work it.

## Why it's Critical
By focusing on one single task at a time, the Engineer Agent ensures maximum quality and prevents "code drift". Any changes made are immediately reflected back in the documentation, keeping the system's "memory" persistent.

## Example Call
> "@EngineerAgent, execute Task [01] from file @T001-reconciliation.md, basing yourself on referenced specification"

