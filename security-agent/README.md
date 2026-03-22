# Security Agent (SecAgent) - The Proactive Guardian

The Security Agent is the "Ethical Hacker" of the ADD pipeline. Its role is to perform continuous security auditing and penetration testing to ensure that the developed software is resilient against attacks and compliant with data protection standards (GDPR, LGPD).

## Responsibilities

-   **SAST (Static Application Security Testing):** Scans the source code for insecure coding patterns, hardcoded secrets, and outdated cryptographic algorithms.
-   **DAST (Dynamic Application Security Testing):** Simulates real-world attacks like SQL Injection, XSS, and IDOR by interacting with the running application.
-   **SCA (Software Composition Analysis):** Audits third-party libraries for known vulnerabilities (CVE) and licensing risks.
-   **Risk Assessment:** Classifies findings using a Severity Matrix (Likelihood x Impact).

## Artifacts

Generates files in `/docs/security/` following the `S00X-name.md` pattern.

## Why it's Critical

The **Security Agent** ensures that security is shifted left in the development lifecycle. By identifying vulnerabilities before code is deployed, it prevents data breaches and ensures compliance with global standards (LGPD, GDPR), protecting both the business and its users.

## Example Call

> "@SecurityAgent, perform a security audit on the new authentication module and generate an S-file with the findings."

---

> *"Security is not a product, but a process." — Bruce Schneier*
