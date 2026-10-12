# Secure Architecture and Threat Analysis – People's Bank Online Banking System
 
![Type](https://img.shields.io/badge/type-security%20architecture-0b5394)
![Domain](https://img.shields.io/badge/domain-banking%20%26%20payments-444)
![Framework](https://img.shields.io/badge/aligned%20with-OWASP%20Top%2010-c00)
![Compliance](https://img.shields.io/badge/compliance-CBSL%20%7C%20Sri%20Lankan%20law-2e7d32)
![Grade](https://img.shields.io/badge/grade-79%2F100%20%28First%20Class%29-gold)
 
A layered security architecture and threat analysis of a Sri Lankan online banking platform: **People's Pay** (mobile wallet), **People's Wave** (mobile banking) and **Internet Banking** (web portal).
 
The analysis looks at the platform end to end. It identifies critical assets and key risks, then defines a testable **security requirements specification (SRS)**. It designs controls for identity, network, platform, application, data, detection, resilience and compliance, and traces every requirement back to the controls that implement it.
 
## Result
 
| | |
|---|---|
| **Grade** | **79 / 100** |
| **Module** | Cyber Security · BSc (Hons) Computing · Coventry University (via NIBM) |
| **Assessment** | Written report (~4,500 words) + viva |
 
> *"A solid and well-rounded submission demonstrating a good understanding of both the security requirements and the deployment environment. The SRS was clearly articulated and Part B showed a thoughtful approach to the security apparatus. The viva performance was strong, reflecting genuine engagement with the material. A commendable piece of work overall."*
> — Instructor feedback
 
The full report is available on request.
 
> **Academic disclaimer:** this is an independent academic analysis completed for the Cyber Security module of the BSc (Hons) Computing programme (Coventry University, UK, via NIBM). It is based only on publicly available information. It is **not affiliated with or endorsed by People's Bank**, and it does **not** describe the bank's actual internal infrastructure or controls. All controls, thresholds and intervals are a *proposed reference design*.
 
---
 
## Result
 
| | |
|---|---|
| **Module** | Cyber Security, BSc (Hons) Computing, Coventry University (via NIBM) |
| **Grade** | **79 / 100 (First Class)** |
| **Assessment** | Written report (38 pages) and viva |
 
> *"A solid and well-rounded submission demonstrating a good understanding of both the security requirements and the deployment environment. The SRS was clearly articulated and Part B showed a thoughtful approach to the security apparatus. The viva performance was strong, reflecting genuine engagement with the material. A commendable piece of work overall."*
>
> — Module instructor
 
The full report is available on request. Contact me via [LinkedIn](https://www.linkedin.com/in/umandi-de-silva-9b88a423b).
 
---
 
## Highlights
 
| Area | What this analysis covers |
|---|---|
| **Result** | **79/100 (First Class)**, with a strong viva |
| **Threat analysis** | 9 critical asset groups, 10 key risks, 13 integrations, including CEFT/LankaPay, core banking, AML and KYC |
| **Security requirements** | 13 requirements across IAM, network, system, application and data layers, each with **pass/fail acceptance tests** |
| **Identity & access** | MFA for all users, RBAC with 6 roles, admin access only over VPN from certificate-verified devices, secrets kept in a vault or HSM |
| **Network** | DMZ, then WAF, then API gateway, then a segmented internal network (application, database, integration and admin zones); TLS 1.2+ everywhere and mTLS for sensitive calls |
| **Application security** | OWASP Top 10 secure coding, parameterised queries, output encoding, short-lived JWTs with refresh-token rotation, CSRF tokens, SAST/DAST in CI/CD |
| **Data protection** | TDE, column-level encryption for NIC, card and account numbers, masking, key rotation in HSM, SHA-256 integrity checks on backups |
| **Detection & response** | SIEM alerting rules, IDS/IPS, fraud monitoring, a 5-step incident response process with CBSL reporting |
| **Resilience** | High-availability design, automatic failover, **RPO 15 minutes / RTO 1–2 hours**, rate limiting |
| **Compliance** | CBSL guidelines plus 6 Sri Lankan Acts, 7-year tamper-proof audit logs |
 
---
 
## Architecture at a glance
 
```mermaid
flowchart TB
    subgraph PUBLIC["🟩 Public Trust Boundary"]
        C["Customers<br/>Web & Mobile"]
        subgraph IAM["IAM Layer"]
            MFA[MFA] --> AUTH[Authentication Server] --> RBAC[RBAC] --> SESS[Session Management]
        end
        subgraph NET["Network Layer"]
            TLS["HTTPS / TLS 1.2+"] --> DMZ[DMZ] --> WAF["WAF (Layer 7)"] --> APIGW[API Gateway] --> FW3["Layer 3 Internal Firewall"]
        end
    end
 
    A["Bank Admin<br/>VPN + MFA + device cert"]
 
    subgraph INTERNAL["🟧 Internal Trust Boundary"]
        subgraph SYS["System Layer"]
            LB[Load Balancer] --> APP1[App Server Node 1]
            LB --> APP2[App Server Node 2]
            ADM[Admin Portal Host]
        end
        subgraph APPL["Application Layer"]
            PUB[Public Endpoints]
            PRIV[Private Endpoints]
            VAL[Input Validation]
            BL[Business Logic]
        end
    end
 
    subgraph RESTRICTED["🟥 Highly Trusted / Restricted Boundary"]
        DB[("Database<br/>Encrypted")]
        CBS[("Core Banking DB<br/>Encrypted")]
        BK[Backup Repository] --> KM["Key Management (HSM/KMS)"]
    end
 
    subgraph EXT["⬜ External Services Boundary"]
        LP[LankaPay / CEFT]
        BILL[Utility & Bill Payments]
        KYC[KYC Provider]
        SMS[SMS / Email Gateway]
    end
 
    C --> IAM
    C --> NET
    A --> IAM
    A --> ADM
    FW3 --> LB
    APP1 --> PUB
    ADM --> PRIV
    PUB --> VAL
    PRIV --> VAL
    VAL --> BL
    BL --> DB
    BL --> CBS
    FW3 --> EXT
 
    style PUBLIC fill:#e8f5e9,stroke:#2e7d32,stroke-dasharray: 5 5
    style INTERNAL fill:#fff3e0,stroke:#ef6c00,stroke-dasharray: 5 5
    style RESTRICTED fill:#ffebee,stroke:#c62828,stroke-dasharray: 5 5
    style EXT fill:#f5f5f5,stroke:#9e9e9e,stroke-dasharray: 5 5
```
 
The full draw.io diagram with icons and trust boundaries is in [`assets/architecture-diagram.png`](assets/architecture-diagram.png). [Architecture](docs/02-architecture.md) explains it in detail.
 
---
 
## Documentation
 
### Part A – Context, risks and requirements
| # | Document | Contents |
|---|---|---|
| 01 | [System Context](docs/01-system-context.md) | Business purpose, the three applications, system tiers, critical assets, roles, integrations |
| 02 | [Architecture](docs/02-architecture.md) | Trust boundaries, layers, request flows, diagram |
| 03 | [Threat Model](docs/03-threat-model.md) | Key risks mapped to affected assets and mitigating controls |
| 04 | [Security Requirements (SRS)](docs/04-security-requirements.md) | 13 requirements with acceptance tests |
 
### Part B – Security controls
| # | Document | Contents |
|---|---|---|
| 05 | [Target Environment & Shared Responsibility](docs/05-shared-responsibility.md) | Hybrid cloud and on-premises split; cloud, on-premises and third-party responsibility matrices |
| 06 | [Identity, AuthN/AuthZ & Secrets](docs/06-identity-access.md) | Identities, customer and admin authentication, RBAC roles, secrets management |
| 07 | [Network & Platform Security](docs/07-network-platform.md) | DMZ, Layer 3 rules, TLS everywhere, zone segmentation, API gateway, CIS hardening |
| 08 | [Application Security Engineering](docs/08-application-security.md) | OWASP secure coding, endpoint segregation, session security, CI/CD security, penetration testing scope |
| 09 | [Data Protection](docs/09-data-protection.md) | Encryption at rest and in transit, key management, backups |
| 10 | [Observability, Detection & Response](docs/10-detection-response.md) | SIEM, dashboards, alert rules, IDS/IPS, fraud monitoring, incident response |
| 11 | [Resilience & Reliability](docs/11-resilience.md) | High availability, failover, disaster recovery targets, rate limits |
| 12 | [Compliance, Privacy & Audit](docs/12-compliance-audit.md) | CBSL, Sri Lankan legislation, privacy principles, audit programme |
| 13 | [Traceability Matrix](docs/13-traceability-matrix.md) | Every SRS requirement mapped to the controls that implement it |
| — | [References](docs/references.md) | Sources |
 
---
 
## Repository structure
 
```
.
├── README.md
├── assets/
│   └── architecture-diagram.png
└── docs/
    ├── 01-system-context.md
    ├── 02-architecture.md
    ├── 03-threat-model.md
    ├── 04-security-requirements.md
    ├── 05-shared-responsibility.md
    ├── 06-identity-access.md
    ├── 07-network-platform.md
    ├── 08-application-security.md
    ├── 09-data-protection.md
    ├── 10-detection-response.md
    ├── 11-resilience.md
    ├── 12-compliance-audit.md
    ├── 13-traceability-matrix.md
    └── references.md
```
 
## Skills demonstrated
 
`Threat modelling` · `Security requirements engineering` · `Defence-in-depth architecture` · `IAM (MFA, RBAC, session management)` · `Network segmentation & zero trust` · `OWASP Top 10` · `Secure SDLC (SAST/DAST)` · `Encryption & key management` · `SIEM & incident response` · `Business continuity / DR` · `Regulatory compliance (CBSL)` · `Requirements traceability`
 
## Author
 
**M. H. T. Umandi de Silva**, BSc (Hons) Computing, Coventry University (NIBM)
[LinkedIn](https://www.linkedin.com/in/umandi-de-silva-9b88a423b) · [GitHub](https://github.com/ThisaruUmandi)
 
---
 
<sub>© M. H. T. Umandi de Silva. Shared for portfolio purposes. Please do not reproduce or submit this work for academic credit.</sub>
 
