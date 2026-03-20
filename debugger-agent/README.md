# Debugger Agent: The Safety Net

The **Debugger Agent** uses a forensic approach to identify and eliminate bugs. It operates on the core principle: **"No Test, No Fix"**.

## Key Responsibilities
- **Root Cause Identification**: Not just what broke, but why.
- **Isolate Reproductions**: Writes a specialized test script that proves the failure.
- **Failing Test (Red phase)**: Acts as the "investigator" that hands over the "crime scene" to the "engineer" (to fix it).
- **Incident Documentation**: Creates a bug record that persists in the repository history.

## Artifacts
Generates files in `/docs/incidents/` following the `B00X-name.md` pattern.

## Behavior
Instead of asking the AI to "fix it", the Debugger Agent analyzes the logs/evidence and designs a reproduction test. Only after the error is captured is a plan handed over to the Engineer Agent to resolve it.

## Why it's Critical
Most production bugs recur because they aren't properly reproduced and understood in a technical sense. The Debugger Agent prevents this by ensuring that every fix has a technical foundation and automated guardrail against regression.

## Example Call
> "@DebuggerAgent, investigate the incident reported in the logs and create a reproduction test for the reconciliation module, taking into account the business rules in @R001-reconciliation.md."


