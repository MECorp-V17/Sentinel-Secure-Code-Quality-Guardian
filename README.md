# MEONEX SECURITY SUITE — CAESAR + BRUTUS + SENTINEL

An evidence-driven, three-role security assurance workflow for web, mobile, desktop, APIs, backend services, databases, cloud infrastructure and software supply chains.

## The three independent roles

- **CAESAR — Red Team Security Assessor:** discovers and safely validates weaknesses across the authorized scope. Produces evidence-based findings and does not change application code.
- **BRUTUS — Remediation Engineer:** independently validates CAESAR findings, fixes confirmed root causes, adds regression/security tests and re-runs relevant checks. Does not approve its own release.
- **SENTINEL — Independent Quality & Release Guardian:** examines functional correctness, privacy, data integrity, regressions and the quality of security evidence. It can block release.

Sentinel's existing root-level SKILL.md is preserved as the general engineering skill. The new SENTINEL folder contains its separate independent release gate.

## Start here

1. Read SHARED/WORKFLOW.md and fill SHARED/ASSESSMENT-SCOPE-TEMPLATE.md.
2. Run CAESAR/SECURITY-AUDIT.md against the explicitly authorized repository, build and environments.
3. Give the complete CAESAR report and exact commit SHA to BRUTUS/REMEDIATION.md.
4. Ask SENTINEL to use the root SKILL.md plus SENTINEL/RELEASE-GATE.md for an independent decision.
5. Record the result using SHARED/RELEASE-CHECKLIST.md.

## Coverage

Stack-adaptive checks include, where present: Android, iOS, Flutter, web, desktop, PHP and Composer, Node.js, Python, Java, .NET, Go, Rust, Ruby, Swift, Kotlin, REST, GraphQL, RPC, WebSockets, webhooks, SQL/NoSQL, PostgreSQL, Supabase, Firebase, object storage, Docker, Kubernetes, serverless, cloud/IaC, DNS/TLS/CDN/WAF, CI/CD, signing, dependencies, SBOM, secrets, AI/LLM systems, privacy, logs and backups.

Agents must discover actual languages, versions, runtime configuration, dependencies and deployed components. The lists of weaknesses and tools are not exhaustive; they must select checks based on the actual attack surface and current vulnerability intelligence.

## Safety and authorization

Only assess assets owned by the operator or explicitly authorized in writing. Prefer source review, local isolated environments, synthetic data and staging. Production dynamic testing requires exact written scope, change-window approval, rate limits, rollback/backup and dedicated test identities. Destructive tests, denial-of-service, credential attacks, persistence, stealth, exfiltration and third-party testing are prohibited by default.

Never print secrets or real personal data. Keep raw sensitive scanner output in approved private storage, not a public repository. Do not run production migrations, rotate live credentials or deploy without explicit authorization.

## Release principle

An unresolved confirmed Critical or High issue, exposed active secret, failed required test, unverified sensitive authorization boundary, or unacceptable critical blind spot blocks release. A check that was not run is NOT TESTED, not PASS. Sentinel's decision applies only to the exact commit, artifact, environment, scope and assessment time.

**No prompt or scanner can guarantee that software is unhackable or that every unknown vulnerability has been found.** A clean result means that the recorded checks found no reportable issue within their documented scope and limitations. Ongoing patching, monitoring, incident response and reassessment remain necessary.

## Repository map

- CAESAR/SECURITY-AUDIT.md — independent security assessment prompt.
- BRUTUS/REMEDIATION.md — fix, regression-test and re-verification prompt.
- SENTINEL/RELEASE-GATE.md — independent release decision prompt.
- SHARED/WORKFLOW.md — operating sequence and responsibilities.
- SHARED/ASSESSMENT-SCOPE-TEMPLATE.md — per-project authorization and coverage input.
- SHARED/SECURITY-STANDARDS.md — standards and weakness taxonomy reference.
- SHARED/VULNERABILITY-INTELLIGENCE.md — current advisory and CVE research procedure.
- SHARED/RELEASE-CHECKLIST.md — reusable release record.
- SKILL.md — preserved Sentinel general engineering skill.

## Use with coding agents

Open the target project in the coding agent and provide the relevant role file. Make the agent report tools actually available, commands actually run, exit codes, target commit and coverage limitations. Do not accept fabricated scan results or a release claim based only on a prompt response.