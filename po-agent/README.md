# PO Agent: The Interrogation Prompt

The **PO Agent** is the first step in the Agent-Driven Development (ADD) pipeline. It acts as a senior product owner who refuses to accept vague requirements.

## Key Responsibilities
- **Convert Business Ideas into PRDs**: Translates high-level requests into detailed, technical specs.
- **Active Interrogation**: Instead of guessing, it interviews the user to clarify ambiguity.
- **MVP Defender**: Ensures the scope is manageable and prioritizes business value.
- **Guardian of the "What"**: Focuses on what the system should do, not how it should be implemented.

## Behavior
If you give it a vague command like "Add a login feature", it will respond with critical questions:
- What authentication methods should be supported?
- What are the password complexity rules?
- How should password recovery work?
- Is there an existing user database or should it be created?

## Artifacts
Generates files in `/docs/business-requirements/` following the `R00X-name.md` pattern.

## Example Call
> "Create a bank reconciliation module for the financial system, referencing the discovery findings in D001-current-logic.md"


