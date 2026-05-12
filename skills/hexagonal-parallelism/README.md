# Hexagonal Parallelism Skill

## Purpose

This skill transforms **Hexagonal Architecture (Ports & Adapters)** from a design pattern into an **industrial parallelism strategy** for Agent-Driven Development.

By enforcing strict boundary isolation and contract-first design, the Architect Agent decomposes work into independent **waves** that multiple Engineer Agents execute simultaneously.

## The Three-Wave Model

```
Wave 1 (Domain Core)    →  Pure entities, value objects, domain services
Wave 2 (Ports & UseCases) →  Interface contracts + application services
Wave 3 (Adapter Explosion) →  REST, JPA, Messaging, External — ALL in parallel
```

## Key Principles

- **Dependency Inversion:** Domain depends on nothing. Adapters depend on Ports.
- **Contract-First:** Ports are fully specified before any adapter is built.
- **Zero Cross-Reference:** No adapter may import another adapter.
- **Wave Isolation:** Tasks within a wave have zero dependencies on each other.

## Result

- **50% reduction** in implementation time through massive parallelism.
- **Parallelism Ratio target:** ≥ 70% of all tasks executable in parallel.

## Usage

The Architect Agent should reference `SKILL.md` when generating any `T00X` Technical Checklist.
