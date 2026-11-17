# Security Release Checklist and Decision Record

Complete for every release candidate. Use actual evidence, never assumptions.

## Candidate identity
- Product/repository:
- Branch and commit SHA:
- Version/build:
- Artifact SHA-256:
- Environment:
- Assessment timestamp and timezone:
- Scope and authorization reference:
- Exclusions:

## Coverage
| Component | In scope? | Exact version/config known? | Tested? | Evidence reference | Limitation |
|---|---|---|---|---|---|
| Web/mobile/desktop client | | | | | |
| Backend/API/GraphQL/RPC | | | | | |
| Authentication/identity | | | | | |
| Database/RLS/grants/functions | | | | | |
| Storage/file/media | | | | | |
| Cloud/IaC/network/TLS/DNS | | | | | |
| Containers/Kubernetes/serverless | | | | | |
| CI/CD/build/signing/artifacts | | | | | |
| Dependencies/runtime/plugins | | | | | |
| PHP/runtime/extensions/CMS, if present | | | | | |
| AI/LLM/tools/vector store, if present | | | | | |
| Logs/analytics/backups/retention | | | | | |
| Third-party integrations | | | | | |

Use N/A only with a reason. Missing evidence is NOT TESTED.

## Required checks
- [ ] Written authorization and exact scope recorded.
- [ ] Same commit SHA and artifact identity across CAESAR, BRUTUS and SENTINEL.
- [ ] Attack surface and data flows mapped.
- [ ] Authentication/session lifecycle reviewed.
- [ ] Object/function/property/tenant authorization verified.
- [ ] Cross-user and cross-role negative tests passed.
- [ ] Database, RLS, grants, RPC, views and storage rules reviewed.
- [ ] Injection/input validation and output handling reviewed.
- [ ] Web/browser/API checks completed where applicable.
- [ ] Android/iOS/mobile platform checks completed where applicable.
- [ ] File/media upload and download access checked.
- [ ] Runtime/framework/plugin/extension versions identified.
- [ ] Current vendor advisories and vulnerability sources checked.
- [ ] SAST/SCA/secret/IaC/container checks run where applicable.
- [ ] SBOM generated or reason not generated recorded.
- [ ] No active secrets exposed in source, artifacts, logs or client bundles.
- [ ] Privacy, retention, deletion, analytics, backups and exports reviewed.
- [ ] Regression/security tests added for confirmed findings.
- [ ] Required formatter/lint/type/build/unit/integration/security tests passed.
- [ ] Failed and unexecuted checks disclosed.
- [ ] No unresolved Critical or High findings.
- [ ] Medium risks have documented authorized acceptance, owner and deadline.
- [ ] Rollback/backup and operational readiness reviewed where relevant.
- [ ] Sentinel independent review completed.

## Findings register
| ID | Severity | Confidence | State | Fix commit | Regression test | Re-scan | Owner/deadline |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

## Evidence register
| Tool/check | Version | Target/commit | Date/time | Command/config | Exit code | Result | Evidence path |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

Do not commit raw sensitive scan output, credentials, tokens, cookies or personal data to a public repository. Store protected evidence in approved private storage.

## Residual risk register
| Risk | Why unresolved | Impact | Mitigation | Authorized owner | Due/review date |
|---|---|---|---|---|---|
| | | | | | |

## Final decision
- [ ] PASS — scoped mandatory checks completed; no unresolved Critical/High or policy blocker.
- [ ] CONDITIONAL PASS — no blocker; residual risks explicitly accepted by authorized owner with mitigation and due date.
- [ ] BLOCKED — blocker, failed required check or critical unassessed area remains.
- [ ] NOT VERIFIED — evidence, scope or test execution insufficient.

- Decision maker:
- Date:
- Evidence links:
- Release conditions:
- Next reassessment date:

The decision applies only to the named commit, artifact, environment, scope and time. It is not a guarantee against unknown vulnerabilities or future changes. Continue patching, advisory monitoring, logging, backup/restore testing and incident response.