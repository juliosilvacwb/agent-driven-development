# Security Agent (SecAgent) — The Proactive Guardian

The Security Agent is the "Ethical Hacker" of the ADD pipeline. Its role is to perform continuous security auditing and penetration testing to ensure that the developed software is resilient against attacks and compliant with data protection standards (GDPR, LGPD).

## Core Philosophy: One Security File per T-File

Similar to the Test Agent, the Security Agent enforces an **Idempotent Upsert Rule**. A single `S00X-name.md` file tracks all vulnerabilities and security checklist items requested across all tasks of a given feature (`T00X-name.md`). It appends new findings to the existing file rather than creating redundant files for every task, maintaining a clean, auditable security log for the Engineer Agent.

## Responsibilities

1. **SAST (Static Application Security Testing):** Scans the source code for insecure coding patterns, hardcoded secrets, and outdated cryptographic algorithms.
2. **DAST (Dynamic Application Security Testing):** Simulates real-world attacks like SQL Injection, XSS, and IDOR by interacting with the running application.
3. **SCA (Software Composition Analysis):** Audits third-party libraries for known vulnerabilities (CVE) and licensing risks.
4. **Idempotent Upsert:** Ensures only one `S00X` file maps to one `T00X` by checking for previously existing audit logs, and adds a `Security Audit` reference link to the original architecture file.
5. **Engineer Checklist Formatting:** Converts risk assessments into actionable task lists (Fix, Location, Validation) for the Developer.

## Operational Workflow

1. **Identify** the source `T00X-name.md` → derive the target `S00X-name.md` filename.
2. **Check** if `S00X-name.md` already exists in `/docs/security/`.
3. **Analyze** the recently implemented task(s) for security flaws.
4. **Create or Append** checklist items to the exact `S00X` file under a dated header.
5. **Back-reference** the S-file inside the source T-file's header.
6. **Confirm** output: files modified, finding items appended, and link created.

## Actionable Artifact Format

| Source File | S-File (Security) | Location |
|---|---|---|
| `docs/architecture/T007-slides.md` | `docs/security/S007-slides.md` | Same number + same name |

## Why it's Critical

The **Security Agent** ensures that security is shifted left in the development lifecycle. By identifying vulnerabilities *before* code is deployed and structuring solutions into explicit Engineer Checklist tasks, it prevents data breaches and guarantees compliance, without breaking the process execution chain.

## Example Call

> "@SecurityAgent, perform a security audit on Task 003 of @T001-reconciliation.md. Create or update the existing S-file with the findings."

---

> *"Security is not a product, but a process." — Bruce Schneier*
