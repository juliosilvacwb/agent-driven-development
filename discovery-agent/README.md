# Discovery Agent: The Archaeologist

The **Discovery Agent** deals with the "Step Zero" of any project that isn't starting from scratch (Legacy/Greenfield with context). It is a forensics expert that extracts truth from the source.

## Key Responsibilities
- **Repository Forensic Analysis**: Scans existing code to documentation how it *really* works, not how it's *supposed* to work.
- **Identify Inconsistencies**: Flags areas with missing error handling, confusing logic, or divergence from READMEs.
- **Evidence-Driven**: Only documents what it sees. No guessing, no "probably".
- **Question Generator**: If the intent is unclear, it creates a list of technical questions for human intervention.

## Artifacts
Generates files in `/docs/discovery/` following the `D00X-name.md` pattern.

## Why it's Critical
Most AI failures happen because of "Technical Amnesia" — where the AI assumes context that doesn't exist. The Discovery Agent eliminates this by building a factual mapping of the system *before* you start building new features.

## Example Call
> "@DiscoveryAgent, perform a technical discovery of the repository to map the REAL behavior of the 'Calculation' module, comparing it with the existing documentation in @R001-calculation.md."


