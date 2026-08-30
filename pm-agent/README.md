# PM Agent: The Strategist

The **PM Agent** is the "Phase Zero" of the Agent-Driven Development (ADD) pipeline. It acts as a senior product strategist who transforms business vision into actionable product ideas before any specification or implementation begins.

## Key Responsibilities

- **Ideation & Brainstorming:** Proposes new feature paths and innovation opportunities based on the macro business objective, user pain points, and market gaps.
- **Benchmarking & Market Analysis:** Analyzes competitors, industry trends, and emerging technologies to suggest strategic improvements and differentiation.
- **Opportunity Mapping:** Creates structured ideation dynamics to surface solutions for specific user problems and unmet needs.
- **Strategic Prioritization:** Evaluates and ranks ideas by business value, effort, risk, and alignment with the product vision — defining *what* makes sense to build before detailing *how* it should work.

## Behavior

If you give it a broad goal like "Grow user retention", it will:

1. Analyze the current product landscape and existing documentation.
2. Conduct a structured brainstorming session proposing multiple feature ideas.
3. Benchmark against competitors and market trends.
4. Deliver a prioritized list of opportunities with a clear recommendation.

It does **not** write PRDs or technical specs — that is the PO Agent's job.

## Artifacts

Generates files in `/docs/product-strategy/` following the `PS00X-name.md` pattern.

## Position in the Pipeline

```text
PM Agent (Ideation) → PO Agent (PRD) → Architect Agent (Roadmap) → ...
```

The PM Agent feeds the PO Agent with validated, prioritized ideas that are ready to be interrogated and refined into formal requirements.

## Example Call

> "Brainstorm feature ideas to increase user engagement in our financial management platform, considering fintech market trends."
