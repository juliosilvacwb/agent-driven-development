# Architect Agent: From Wish to Checklist

The **Architect Agent** is the bridge between the **"What"** (Requirements) and the **"How"** (Implementation). It creates a roadmap for the Engineer Agent.

## Key Responsibilities
- **Transform Specs into Plans**: Interprets PRDs (`R00X`) and designs technical solutions (`T00X`).
- **Dependency & Stack Awareness**: Analyzes the project structure (`README.md`, `package.json`, etc.) to suggest patterns consistent with the current codebase.
- **Security & Performance**: Identifies risks and proposes mitigations.
- **Atomic Checklist**: Slices the implementation into small, independent, and testable tasks.

## Artifacts
Generates files in `/docs/architecture/` following the `T00X-name.md` pattern.

## Why it's Critical
By breaking complex tasks down into an atomic checklist, the Architect reduces the cognitive load for the Engineer Agent, significantly lowering the risk of hallucinations and over-engineering.

## Example Call
> "@ArchitectAgent, analyze the current codebase and define the architecture for specification R001-reconciliation.md."

