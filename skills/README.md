# ADD Skills

Skills are reusable packages of knowledge that extend agent capabilities beyond their base prompts. Each skill provides specialized instructions, patterns, and conventions that agents apply during their workflow.

## Available Skills

| Skill | Description | Primary Consumer |
|-------|-------------|-----------------|
| [hexagonal-parallelism](./hexagonal-parallelism/) | Hexagonal Architecture as an industrial parallelism strategy. Maximizes decoupling to enable parallel task execution by AI agents. | Architect Agent |

## Structure

Each skill directory contains:

- **`SKILL.md`** (required): The main instruction file with YAML frontmatter and detailed guidance.
- **`README.md`**: Human-readable overview of the skill's purpose and usage.
- **`examples/`** (optional): Reference implementations and usage patterns.
- **`resources/`** (optional): Templates, diagrams, or other assets.

## How Skills Are Used

1. The **Architect Agent** (or any relevant agent) checks available skills before generating its output.
2. If a skill is relevant to the current task, the agent reads the `SKILL.md` and follows its instructions.
3. Skills influence the structure, patterns, and conventions applied to the generated artifacts.
