# 03 · Threat Model

[← Architecture](02-architecture.md) · [README](../README.md) · Next: [Security Requirements →](04-security-requirements.md)

## Key risks

| ID | Risk | Assets at risk | Mitigating controls | Related SRS |
|---|---|---|---|---|
| R1 | **Account takeover** through phishing, credential attacks and social engineering | Credentials, authentication factors, accounts | MFA for all users, OTP for sensitive actions, rate-limited login, short-lived JWTs, invalidation on suspicious activity | IAM-01, IAM-03, NET-02 |
| R2 | **Data breaches** | PII, account and transaction data | Network segmentation, no public database ports, TDE and column-level encryption, masking | NET-01, NET-03, DATA-01 |
| R3 | **Unauthorised or fraudulent transactions** | Accounts, transactions | MFA/OTP on transfers, transfer rate limits, fraud monitoring, SIEM alerts on unusual transfer spikes | IAM-01, NET-02, SYS-02 |
| R4 | **PII or financial data theft** | PII, card data | Column-level encryption, masking, least-privilege RBAC, access logging | IAM-02, DATA-01, DATA-02 |
| R5 | **Compromise of APIs or third-party integrations** | Integration credentials, transactions | API gateway enforcement, integration zone, TLS, managed API keys, allow-lists, input and output validation | NET-02, NET-03, APP-01, APP-02 |
| R6 | **Insider misuse of privileged access** | All data, admin console | RBAC with separation of duties, VPN + MFA + device certificates, SIEM alerts on after-hours admin activity, tamper-proof audit logs | IAM-02, SYS-02 |
| R7 | **Malware / ransomware** | Infrastructure, backups | CIS hardening, patch management, IDS/IPS, encrypted off-site backups, restore drills | SYS-01, DATA-03 |
| R8 | **Privacy leaks** | PII, logs | Data minimisation, no secrets or PII in logs, consent-based sharing, access recording | APP-02, DATA-01 |
| R9 | **DDoS attacks** | Availability | Cloud DDoS protection, WAF, rate limiting, load balancing, auto-scaling | NET-02 |
| R10 | **Backup or recovery failure** | Backups and DR artefacts | Daily incremental and weekly full backups, SHA-256 integrity checks, quarterly restore drills, DR site | DATA-03 |

## Attack surface

| Surface | Exposure | Primary protection |
|---|---|---|
| Web portal and mobile apps | Internet | WAF, TLS, MFA, rate limiting |
| Public API endpoints (`/login`, `/register`, `/transfer`, `/profile/update`) | Internet | API gateway, token validation, input validation |
| Private endpoints (`/admin/*`, `/internal/*`) | Internal only | VPN, mTLS, RBAC, IP allow-lists |
| Third-party integrations | Partner networks | Integration zone, TLS, API keys, allow-lists |
| Staff / admin accounts | Internal | VPN, MFA/TOTP, device certificates, SIEM |
| Backups | Off-site | Encryption, integrity checks |

See [Traceability Matrix](13-traceability-matrix.md) for how each requirement is implemented.
