# Quality Agent: The Gatekeeper

The **Quality Agent** acts as the final arbiter of truth. It does not just check if the code "works" (that's the unit test's job); it checks if the code is **correct** relative to the project's intent and standards.

## Key Responsibilities
- **Cross-Validation**: Compares the implementation with the requirement (`R`) and the architecture plan (`T`).
- **Security Audit**: Scans for vulnerabilities, hardcoded secrets, and performance bottlenecks.
- **Micro-Code Review**: Rejects "gold plating" (unrequested features) and ensures Clean Code/SOLID principles.
- **Fidelity Check**: Confirms that test coverage is not superficial and adequately handles edge cases and errors.

## Workflow
1. Analyze the proposed code alongside `R-` and `T-` files.
2. Provide precise technical feedback for corrections.
3. Once satisfied, respondent with `APPROVED` and updates the `T-` file status to `[APPROVED]`.

## Why it's Critical
Even specialized agents can drift. The Quality Agent forces a sanity check before code is merged, ensuring that the project does not accumulate technical debt or unrequested complexity.

## Example Call
> "@QualityAgent, review the code for Task [01] of @T001-reconciliation.md comparing with requirement, tests and security specification. Verify if all implementation are correct."

