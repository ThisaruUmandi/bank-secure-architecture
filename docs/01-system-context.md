# 01 · System Context

[← Back to README](../README.md) · Next: [Architecture →](02-architecture.md)

## Business purpose

| | |
|---|---|
| **Industry** | Banking |
| **System** | People's Bank Online Banking System |

The online banking system lets retail and business customers do everyday banking securely without visiting a branch. It is delivered through web and mobile channels built around three applications:

| Application | Channel | Purpose |
|---|---|---|
| **People's Pay** | Mobile | Mobile wallet for sending money, paying merchants and QR payments |
| **People's Wave** | Mobile | Personal banking: accounts, transfers, bills and cards |
| **Internet Banking** | Web | Browser-based portal for banking operations |

## System tiers

### 1. User interface (client layer)
Lets users interact with the banking system securely.

| Feature | Mobile app (Android / iOS) | Web portal |
|---|---|---|
| Login | ✅ | ✅ |
| Password / PIN | ✅ | ✅ |
| Biometrics | ✅ | ❌ |
| Transfer screens | ✅ | ✅ |
| Payment screens | ✅ | ✅ |
| Transaction confirmation screens | ✅ | ✅ |
| QR scanner | ✅ | ❌ |

### 2. Server logic (application layer)
Processes requests securely and applies business rules and banking logic. It consists of **API gateways** and **application servers**.

### 3. Database (data layer)
Keeps personally identifiable information (PII) and sensitive financial data confidential, accurate and available:
- Customer details
- Account balances
- Transaction history
- Card information
- Loan details
- Login and device logs
- Audit trails

## Critical assets

| # | Asset group | Examples |
|---|---|---|
| 1 | **User credentials** | User ID, password |
| 2 | **Authentication factors** | Biometric identifiers, MFA tokens, device bindings |
| 3 | **Account & transaction data** | Balances, transaction history, standing orders |
| 4 | **PII** | NIC number, contact details, PAN, account number |
| 5 | **Application secrets & keys** | Database credentials, API keys, HSM- and KMS-managed root keys, TLS certificates |
| 6 | **External integration credentials** | LankaPay/CEFT credentials, biller API keys, card network credentials |
| 7 | **Audit & security logs** | Used for compliance and dispute resolution |
| 8 | **Backups & DR artefacts** | Encrypted snapshots, off-site backups |
| 9 | **Operational infrastructure** | Network devices, WAF, SIEM, admin console |

## Primary roles

| Role | Type | Description |
|---|---|---|
| **Customer** | External | Web and mobile users |
| **Admin** | Internal | Bank staff who manage the online banking system |

[Identity, AuthN/AuthZ & Secrets](06-identity-access.md) breaks these down into detailed RBAC roles.

## Key integrations

1. SMS and email notifications
2. SMS / OTP gateway
3. Card management
4. QR payment network
5. Identity verification and KYC provider
6. Fraud detection and risk analytics
7. Loan management system
8. **LankaPay / CEFT** (interbank switch)
9. Utility and bill payment aggregators
10. **Core banking system (CBS)**
11. Exchange rate provider
12. **AML (anti-money laundering) system**
13. SIEM / audit logging system

### Key external integrations
- **LankaPay / CEFT interbank switch:** enables transfers to other banks. Without it, customers could only transfer between People's Bank accounts.
- **Utility and bill payment providers:** let customers pay bills in the app, e.g. CEB, LECO, SLT, the Water Board, and mobile bills and reloads.
