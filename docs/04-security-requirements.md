# 04 · Security Requirements Specification (Mini SRS)

[← Threat Model](03-threat-model.md) · [README](../README.md) · Next: [Shared Responsibility →](05-shared-responsibility.md)

Every requirement has a **measurable acceptance test** with a clear pass/fail result.

## IAM layer

### IAM-01 · MFA for all users (customers and admins)
| Test | Expected result |
|---|---|
| Log in with a username and password only | ❌ Authentication **fails** |
| Log in with a username, password and OTP / SMS / app token | ✅ Authentication **succeeds** |

### IAM-02 · Role-based access
| Test | Expected result |
|---|---|
| A customer requests `/admin/*` | ❌ Access **denied** |
| An admin requests `/transfer` | ❌ Access **denied** |

### IAM-03 · Session management
| Test | Expected result |
|---|---|
| Leave the application idle for the configured timeout | User is **logged out automatically** |
| Reuse a session token after logout | ❌ Token **rejected** |

## Network layer

### NET-01 · The database must not expose any port to the public
| Test | Expected result |
|---|---|
| Port scan from an external network | Database ports are **closed or not visible** |

### NET-02 · WAF and rate limiting
| Test | Expected result |
|---|---|
| Send 20 login attempts in 5 seconds | WAF **rate-limits or blocks** |
| Send an SQL injection payload | WAF **blocks** the request |

### NET-03 · Segmented network zones
| Test | Expected result |
|---|---|
| Try to reach the data layer directly from the DMZ | ❌ Connection **fails** |

## System layer

### SYS-01 · Hardened servers
| Test | Expected result |
|---|---|
| Run a CIS Benchmark scan | **No high-severity failures** |

### SYS-02 · Monitoring and logging
| Test | Expected result |
|---|---|
| Trigger a failed login | Event appears in the SIEM **within 30 seconds** |
| Modify a system file | **Alert** raised in the SIEM |

## Application layer

### APP-01 · Input validation and output encoding
| Test | Expected result |
|---|---|
| Submit an invalid payload | API **rejects** it with `400 Bad Request` or a validation error |

### APP-02 · Secrets from a secure vault
| Test | Expected result |
|---|---|
| Inspect the code repository | **No secrets** found |
| Inspect the logs | **No secrets** printed |

## Data layer

### DATA-01 · Encryption at rest and in transit
| Test | Expected result |
|---|---|
| Disable encryption and attempt to start the database | Database **refuses** to run unencrypted |
| Connect to the database without TLS | ❌ Connection **fails** |

### DATA-02 · Key management and rotation
| Test | Expected result |
|---|---|
| Check the KMS logs | Rotation events appear **at the required intervals** |

### DATA-03 · Backups and restore testing
| Test | Expected result |
|---|---|
| Restore a backup to a test environment | Data **matches** the production snapshot |
| Inspect the backup files | Files are **encrypted** |

## Summary

| Layer | Requirements |
|---|---|
| IAM | IAM-01, IAM-02, IAM-03 |
| Network | NET-01, NET-02, NET-03 |
| System | SYS-01, SYS-02 |
| Application | APP-01, APP-02 |
| Data | DATA-01, DATA-02, DATA-03 |
| **Total** | **13** |
