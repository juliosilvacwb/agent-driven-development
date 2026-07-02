# PO Agent: The Interrogation Prompt

The **PO Agent** is the specification stage of the Agent-Driven Development (ADD) pipeline. It acts as a senior product owner who refuses to accept vague requirements.

## Input Sources

The PO Agent can be triggered from two distinct sources:

1. **Direct Chat Request:** The user describes a business idea or feature request directly in the conversation.
2. **Product Strategy Recommendation (PS-file):** The PM Agent delivers a prioritized recommendation via a `PS00X-name.md` file, and the PO Agent uses it as the starting point for a PRD.

## Key Responsibilities

- **Convert Business Ideas into PRDs**: Translates high-level requests — whether from a user or a PS-file — into detailed, technical specs.
- **Active Interrogation**: Instead of guessing, it interviews the user to clarify ambiguity.
- **MVP Defender**: Ensures the scope is manageable and prioritizes business value.
- **Guardian of the "What"**: Focuses on what the system should do, not how it should be implemented.
- **Traceability**: When sourced from a PS-file, maintains a traceable link back to the strategy document.

## Behavior

If you give it a vague command like "Add a login feature", it will respond with critical questions:

- What authentication methods should be supported?
- What are the password complexity rules?
- How should password recovery work?
- Is there an existing user database or should it be created?

If it receives a PS-file recommendation, it will read the strategic context first and then refine the idea into a full PRD.

## Artifacts

Generates files in `/docs/business-requirements/` following the `R00X-name.md` pattern.

## Example Calls

> Direct: "Create a bank reconciliation module for the financial system, referencing the discovery findings in D001-current-logic.md"

> From PM Agent: "Create a PRD for the Smart Notifications feature based on PS001-engagement-features.md, Recommendation #2"


