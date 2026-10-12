# 09 · Data Protection

[← Application Security](08-application-security.md) · [README](../README.md) · Next: [Detection & Response →](10-detection-response.md)

## 1. Encryption at rest
| Control | Detail |
|---|---|
| **Transparent Data Encryption (TDE)** | Encrypts the whole database |
| **Column-level encryption** | Extra protection for NIC, card and account numbers |
| **Masking** | Shows only part of an account or phone number (e.g. `•••• •••• 4821`) |
| **Encrypted log volumes** | Log files sit on encrypted disks |

## 2. Encryption in transit
| Control | Detail |
|---|---|
| **TLS 1.2+** | All traffic between the web portal, mobile apps, APIs and backend |
| **Mutual TLS (mTLS)** | Client and server both authenticate; used for admin and internal systems |
| **Certificate rotation** | Certificates replaced **every 6 months** |

## 3. Key management and rotation
| Control | Detail |
|---|---|
| Storage | Keys held in an **HSM** or secure key vault |
| Rotation | Keys expire and rotate **automatically** |
| Key separation | **Separate keys** for encryption, signing and TLS, so one compromised key doesn't expose the others |

## 4. Backups and recovery
| Control | Detail |
|---|---|
| Daily incremental backups | Capture the day's changes |
| Weekly full backups | Complete database copy |
| Off-site DR location | Copies stored in a separate secure site |
| **SHA-256 integrity checks** | Confirm backups have not been altered |
| **Quarterly restore drills** | Prove that backups can actually be restored |
