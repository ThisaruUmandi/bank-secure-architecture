# 11 · Resilience & Reliability

[← Detection & Response](10-detection-response.md) · [README](../README.md) · Next: [Compliance & Audit →](12-compliance-audit.md)

## High availability
| Control | Purpose |
|---|---|
| Load balancer in the DMZ | Spreads traffic so no single server is overloaded |
| Redundant application servers | Another node takes over if one crashes |
| Database primary–replica | The replica stays ready for failover |
| Active–passive DR site | Standby site activated during a major outage |

## Failover strategy
| Control | Behaviour |
|---|---|
| Auto-scaling application servers | More servers start automatically as traffic rises |
| Synchronous database replication | Data is copied in real time |
| Core banking retry queues | Transactions are held and retried if core banking is unavailable |
| Backup SMS gateway | OTPs go through another provider or email if the SMS provider fails |
| Automatic DNS failover | Traffic moves to a healthy site without interrupting users |

## Disaster recovery targets
| Metric | Target |
|---|---|
| **RPO** (recovery point objective) | Up to **15 minutes** of data loss |
| **RTO** (recovery time objective) | Full service restored within **1–2 hours** |
| DR testing | **Twice a year** |
| Offline encrypted backup retention | **6 months** |

## Performance and rate limiting
| Limit | Threshold |
|---|---|
| Login attempts | **5 per minute** (brute-force protection) |
| Fund transfer attempts | **3 per minute** |
| API throttling | Per IP / device (bot and overload protection) |
