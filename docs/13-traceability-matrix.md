# 13 · Traceability Matrix

[← Compliance & Audit](12-compliance-audit.md) · [README](../README.md) · [References →](references.md)

Every requirement in the [SRS](04-security-requirements.md) is mapped to the controls that implement it.

| SRS ID | Requirement | Implemented controls | Detail |
|---|---|---|---|
| **IAM-01** | MFA for all users | **Customers:** password + OTP, biometrics on mobile · **Admins:** MFA (TOTP) over VPN, device certificates | [06](06-identity-access.md) |
| **IAM-02** | Role-based access | RBAC. Customer roles: Regular, Staff-Customer · Admin roles: System Admin, Fraud Analyst, Customer Support Officer, Audit Officer | [06](06-identity-access.md) |
| **IAM-03** | Session management | Auto logout on inactivity · reused session tokens rejected · refresh-token rotation · CSRF tokens · invalidation on suspicious activity | [08](08-application-security.md) |
| **NET-01** | Database not exposed to the public | Layer 3 firewall · no direct access from the DMZ or internet · admin access only via approved VPN/IP | [07](07-network-platform.md) |
| **NET-02** | WAF + rate limiting | WAF in the DMZ · rate limits on logins, transactions and API calls · SQLi and malicious payloads blocked · endpoint segregation · TLS everywhere | [07](07-network-platform.md), [11](11-resilience.md) |
| **NET-03** | Segmented network zones | DMZ, application, database, integration and admin zones · Layer 3 firewall rules · API gateway enforcement | [07](07-network-platform.md) |
| **SYS-01** | Hardened servers | CIS Benchmark hardening · only required services installed | [07](07-network-platform.md) |
| **SYS-02** | Monitoring and logging | SIEM log collection · real-time dashboards · alerts on logins and failed logins · alerts on file modification | [10](10-detection-response.md) |
| **APP-01** | Input validation and output encoding | OWASP Top 10 aligned · input validation and sanitisation · parameterised queries · output encoding · SAST and DAST | [08](08-application-security.md) |
| **APP-02** | Secrets from a secure vault | All secrets in a vault or HSM · automatic 90-day rotation · database credentials fetched at runtime · managed TLS certificates | [06](06-identity-access.md) |
| **DATA-01** | Encryption at rest and in transit | TDE · column-level encryption · masking · encrypted log volumes · TLS 1.2+ · mTLS for admin and internal traffic | [09](09-data-protection.md) |
| **DATA-02** | Key management and rotation | Keys in an HSM or vault · automatic rotation · separate keys for encryption, signing and TLS | [09](09-data-protection.md) |
| **DATA-03** | Backups and restore testing | Daily incremental and weekly full backups · off-site DR · SHA-256 integrity checks · quarterly restore drills | [09](09-data-protection.md) |

**Coverage:** 13 of 13 requirements are traced to implemented controls ✅
