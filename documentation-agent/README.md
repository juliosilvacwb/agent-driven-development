# Documentation Agent: The Guardian of Truth

The **Documentation Agent** closes the loop in the ADD pipeline. Its job is to eliminate **Documentation Debt** and ensure that the "living memory" of the project remains accurate and easy to consult.

## Key Responsibilities
- **Eliminate Debt**: Synchronizes the Business Spec (`R`), the Architecture Plan (`T`), and the final Implementation (Code).
- **Project Documentation Update**: Edits `README.md`, `CHANGELOG.md`, and any other core project docs.
- **Mermaid Visualizations**: Generates and updates sequence diagrams, flowcharts, and ER diagrams.
- **API and Contract Sync**: Ensures that Request/Response payloads in documentation match reality.

## Behavior
Once a task or a feature sprint is finalized and approved, the Documentation Agent is triggered. It acts as a final audit that everything is documented correctly, in clear terms, and following the single source of truth.

## Why it's Critical
Without documentation, a project eventually becomes a "legacy monster". By forcing every technical evolution through a documentation sync, we ensure the next developer (and AI) has the correct context to continue building safely.

## Example Call
> "@DocumentationAgent, all tasks of @T001-reconciliation.md have been completed and reviewed. Update the project's README.md and generate the sequence diagram for the new feature based on the final code and specification @R001-reconciliation.md"


