# Security Assessment Scope — Fill Before Each Run

Complete this document for each application/release. Do not begin active testing until authorization and exact scope are clear.

## Project identity
- Product/application:
- Repository URL:
- Branch:
- Baseline commit SHA:
- Release/version/build:
- Artifact SHA-256 (if available):
- Technology/runtime versions known:
- Assessment owner/contact:
- Assessment date/time/timezone:

## Environment and authorization
- Environment: LOCAL / ISOLATED TEST / STAGING / PRODUCTION
- Written authorization reference:
- Assets explicitly in scope (exact domains, APIs, apps, cloud account/project IDs, IPs):
- Explicit exclusions:
- Third-party providers separately authorized (if any):
- Allowed methods:
- Prohibited methods:
- Test window:
- Maximum request rate / concurrency:
- Emergency stop contact:
- Backup and rollback verified:
- Production dynamic testing approved? YES / NO

## Test identities
| Identity | Test account reference (no password/token) | Role/tenant | Intended permissions |
|---|---|---|---|
| Anonymous | | | |
| User A | | | |
| User B | | | |
| Moderator | | | |
| Administrator | | | |
| Service identity | | | |

## Components to assess
- [ ] Web client
- [ ] Android application
- [ ] iOS application
- [ ] Flutter / desktop application
- [ ] Backend services
- [ ] REST / GraphQL / RPC / WebSocket APIs
- [ ] Authentication / identity provider
- [ ] Database / RLS / stored procedures
- [ ] File, media and object storage
- [ ] Cloud / infrastructure / IaC
- [ ] Docker / Kubernetes / serverless
- [ ] DNS / TLS / CDN / WAF
- [ ] CI/CD / build / signing / artifacts
- [ ] Runtime / frameworks / packages / plugins
- [ ] Third-party integrations
- [ ] AI / LLM / agents / vector store
- [ ] Logs / analytics / backups / monitoring

## Data and business sensitivity
- Data classes present:
- Personal/sensitive data types:
- Payment/financial operations:
- Location/media/private content:
- Tenant/organization boundaries:
- Retention/deletion/export requirements:
- High-impact operations:
- Regulatory/contractual requirements:

## Tool and environment availability
| Tool/service | Version | Access level | Available? | Limitations |
|---|---|---|---|---|
| Source repository | | | | |
| SAST | | | | |
| SCA / advisory feeds | | | | |
| Secret scanning | | | | |
| DAST / API testing | | | | |
| Mobile analysis | | | | |
| IaC / container / cloud scan | | | | |
| Database policy testing | | | | |
| Runtime/deployment config | | | | |

## Approval
- Scope approved by:
- Approval date:
- Allowed test period:
- Conditions/limitations:

Do not include credentials, tokens, production secrets or real personal data in this file.