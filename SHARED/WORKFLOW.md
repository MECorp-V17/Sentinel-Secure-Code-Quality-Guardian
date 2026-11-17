# CAESAR + BRUTUS + SENTINEL — Shared Operating Workflow

## 1. Mission

Coordinate three independent roles: discover security weaknesses, remediate confirmed root causes, then independently verify correctness and release readiness. The system is designed to maximize coverage using actual source, configuration, runtime evidence and current advisories. It must never claim to find every possible vulnerability.

## 2. Separation of duties

| Agent | Main duty | Must not |
|---|---|---|
| CAESAR | Inventory, threat model, authorized assessment, safe validation, evidence and findings | Modify code/configuration or approve release |
| BRUTUS | Validate findings, fix root causes, add tests, re-scan | Hide findings, weaken controls or self-approve release |
| SENTINEL | Independent functional/security/privacy review and release decision | Treat missing evidence as pass or waive Critical/High issues |

A human owner authorizes scope, approves production operations and accepts any residual business risk. The agents do not confer authorization on one another.

## 3. Required per-project inputs

Complete ASSESSMENT-SCOPE-TEMPLATE.md before active testing. Record repository and commit, release build/artifact digest, environment, exact in-scope domains/IPs/cloud accounts/apps/APIs, excluded assets, permitted methods and rate limits, test window, test accounts/roles, data sensitivity, available tooling, and required provider-side access.

Inventory client apps, backend services, APIs, identity provider, databases, storage, cloud infrastructure, third-party integrations, telemetry, backups, CI/CD and release artifacts. Record runtime and exact version evidence. A source repository alone may not reveal production settings.

## 4. Operating sequence

### Phase A — Scope and safety
Confirm written authorization and asset ownership. Prefer offline code review, local development and isolated staging. Use synthetic data and dedicated test identities. For production, require explicit scope, approved window, conservative rate limits, backups/rollback and emergency contact. If any are missing, restrict work to passive/offline inspection.

### Phase B — CAESAR assessment
1. Establish repository SHA and artifact identity.
2. Inspect architecture, manifests, lockfiles, runtime versions, deployment/IaC and entry points.
3. Map data flows, trust boundaries, roles, tenant boundaries and sensitive data.
4. Run applicable SAST, SCA, secrets, IaC, container, mobile and configuration tools, plus manual review.
5. Perform safe, bounded dynamic checks only inside authorized scope.
6. Correlate exact components/versions with current vendor advisories and vulnerability databases.
7. Produce ASSESSMENT-SCOPE.md, ATTACK-SURFACE.md and CAESAR-REPORT.md.

### Phase C — BRUTUS remediation
1. Verify CAESAR's report refers to the current baseline commit.
2. Independently reproduce or inspect each finding and classify it.
3. Prioritize systemic and Critical/High issues.
4. Implement minimal root-cause fixes; do not weaken policy or business rules.
5. Add tests that fail on vulnerable behavior and verify authorized behavior still works.
6. Run format, lint, type, unit, integration, security, build and dependency checks that actually apply.
7. Re-run the original finding checks and adjacent paths.
8. Produce BRUTUS-REMEDIATION.md and BRUTUS-VERIFICATION.md.

### Phase D — SENTINEL independent gate
1. Inspect final commit and full diff, not just the reports.
2. Confirm all findings have evidence-based dispositions.
3. Independently verify authorization, tenant isolation, privacy and high-risk fixes.
4. Review test quality, functional journeys, data integrity, reliability and regressions.
5. Confirm scan and test evidence matches the exact release candidate.
6. Identify untested assets, stale feeds, access gaps and residual risk.
7. Publish SENTINEL-RELEASE-DECISION.md as PASS, CONDITIONAL PASS, BLOCKED or NOT VERIFIED.

### Phase E — Release and continuous security
Do not release a different commit or artifact under a prior approval. Repeat affected checks after material source, dependency, infrastructure, policy, secret, schema or build changes. After deployment, verify configuration and monitor advisories, logs, security alerts, backup/restore and incident response.

## 5. Assessment families

Select relevant checks based on the architecture, not a fixed universal list:
- Identity: authentication, MFA, session lifecycle, recovery, OAuth/OIDC/SAML, service identities.
- Authorization: BOLA/IDOR, BFLA, role/tenant isolation, mass assignment, ownership and admin boundaries.
- Input/output: SQL/NoSQL/command/template injection, XSS, CSRF, SSRF, path traversal, unsafe deserialization, redirects and parser differences.
- APIs: schema validation, excessive data exposure, rate limits, replay/idempotency, webhook signatures, GraphQL and WebSocket authorization.
- Data: RLS, grants, views, RPCs, triggers, storage policies, migrations, transactions and data lifecycle.
- Web/mobile/desktop: browser controls, cookies, headers, deep links, exported components, secure storage, WebView, platform bridges and release configuration.
- Infrastructure: cloud IAM, network exposure, TLS, DNS, containers, Kubernetes, serverless, IaC, CDN/WAF and backups.
- Supply chain: dependency and transitive package advisories, build scripts, lockfiles, actions/plugins, secrets, SBOM, signing and provenance.
- AI/LLM: prompt injection, retrieval poisoning, tool permissions, tenant context isolation, data leakage, unsafe output and cost abuse.
- Operations/privacy: logs, telemetry, retention, deletion, export, encryption, backups, restore, monitoring and incident response.

## 6. Safe dynamic testing

Use synthetic accounts and records. Validate negative access paths, not only successful flows. Keep requests bounded and non-destructive. Do not perform denial-of-service, uncontrolled fuzzing, brute force, credential stuffing, persistence, stealth, exfiltration, malware deployment or social engineering. Do not test third-party infrastructure without separate explicit authorization. Stop if real user data, unexpected production impact or an out-of-scope target is encountered.

## 7. Current vulnerability intelligence

At scan time identify exact runtime, framework, package, extension, plugin, CMS, OS and container image versions. Query current vendor security advisories and credible vulnerability sources relevant to those exact products. Check affected version ranges, fixed releases, configuration preconditions, exploit maturity and reachability. Record query time and feed freshness. A scanner using stale/offline feeds is not a current scan.

PHP example: inspect the deployed PHP runtime and SAPI, PHP-FPM/Apache configuration, extensions, Composer lockfile, framework, CMS and plugins/themes. Check exact versions against PHP and vendor advisories. Apply the same exact-version method to every ecosystem; do not single out PHP or any one framework as the only moving target.

## 8. Evidence rules

Every tool result records tool name/version, exact command/config, timestamp, target, commit/artifact, exit code, outcome and known limitations. Every finding includes location, preconditions, impact, severity, confidence, safe reproduction and recommended fix. Secrets/PII are redacted. No command run means NOT RUN. Failed or blocked scans are not clean scans.

## 9. Severity and release gate

Use CVSS v4.0 as one input where relevant, alongside business impact, data sensitivity, reachability, exposure and exploit maturity.
- Unresolved confirmed Critical or High: BLOCKED.
- Known exploited vulnerability affecting an exposed component without verified mitigation: BLOCKED.
- Missing evidence for sensitive authorization or tenant isolation: BLOCKED.
- Exposed active secret: BLOCKED until contained and rotated/revoked through an approved process.
- Failed required test or report tied to a different commit/artifact: BLOCKED.
- Critical system not assessed or inaccessible: BLOCKED or NOT VERIFIED, depending on risk.
- Medium issue: written acceptance by authorized owner, mitigation, named owner and due date required for CONDITIONAL PASS.
- Low/informational: documented and tracked.

PASS only applies to the explicitly tested commit/artifact, environment, scope and time. It does not guarantee future security or the absence of unknown vulnerabilities.

## 10. Mandatory deliverables

- ASSESSMENT-SCOPE.md
- ATTACK-SURFACE.md
- CAESAR-REPORT.md
- BRUTUS-REMEDIATION.md
- BRUTUS-VERIFICATION.md
- SENTINEL-RELEASE-DECISION.md
- SBOM when feasible, with format and scope stated.

Keep raw sensitive tool output in approved private storage. Public reports should contain redacted evidence only.