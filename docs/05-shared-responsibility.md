# 05 · Target Environment & Shared Responsibility

[← Security Requirements](04-security-requirements.md) · [README](../README.md) · Next: [Identity & Access →](06-identity-access.md)

## Target environment: hybrid cloud and on-premises

A hybrid model is a practical choice for large banks. Internet-facing traffic management goes to the cloud, and core banking stays on-premises.

| Cloud | On-premises |
|---|---|
| Web frontend and mobile app gateways | Core banking services and application servers |
| Content delivery network (CDN) | Internal APIs and internal service bus |
| WAF and DDoS protection | Account and transaction databases |
| Traffic routing and monitoring | HSM modules for card and PIN operations |

## Shared responsibility matrices

### Cloud provider ↔ bank
| Cloud provider | Bank |
|---|---|
| Physical servers, network and cloud platform | Secure frontend applications and API gateways |
| OS-level hardening | WAF configuration |
| Patch management | TLS enforcement |
| CDN | IAM / SAML policies |
| Traffic routing | Traffic monitoring and log analysis |
| DDoS protection | Alert response; DDoS and WAF tuning; access control |

### On-premises infrastructure ↔ bank
| Infrastructure | Bank |
|---|---|
| Servers, storage, network and physical security | Core banking operations and databases |
| Backup infrastructure | Database backups and DR tests |
| OS and network security | OS hardening, application patching, user access management |

### External service providers ↔ bank
| External provider | Bank |
|---|---|
| Securing their own APIs | Securing internal integrations and connections |
| Service uptime and performance | Validating and sanitising inputs and outputs; monitoring integration failures |
| Protecting their infrastructure | Enforcing TLS, managing API keys, maintaining allow-lists |
