# MantisBT → MantisHub Enterprise Migration Proposal

**Project Scope**  
Validate that MantisHub can fully replace our self-hosted (on-prem) MantisBT—matching functionality, performance, security, and compliance—so we can justify an Enterprise subscription.

---

## Table of Contents
1. [Environment Parity](#1-environment-parity)  
2. [Trial Terms & Conditions](#2-trial-terms--conditions)  
3. [Enterprise Subscription Highlights](#3-enterprise-subscription-highlights)  
4. [Key Differences — Why On-Prem Is Outdated](#4-key-differences--why-on-prem-is-outdated)  
5. [Cross-Team Access & Compliance](#5-cross-team-access--compliance)  
6. [Single Sign-On (SSO) Integration](#6-single-sign-on-sso-integration)  
7. [Customizations & Plugin Audit](#7-customizations--plugin-audit)  
8. [Migration Mechanisms](#8-migration-mechanisms)  
9. [Detailed Migration Tasks](#9-detailed-migration-tasks)  
10. [Operational Considerations](#10-operational-considerations)  
11. [Conclusion & Final Assessment](#11-conclusion--final-assessment)  

---

## 1. Environment Parity
- **Version Match** – Select identical major.minor release (e.g., 2.25.10).  
- **Schema & Custom Tables** – `mysqldump --no-data` all `mantis_*` + integration tables; import to cloud.  
- **Plugins** – List from `mantis_plugin_table`; upload/enable each in MantisHub.  
- **Config** – Export key rows from `mantis_config_table`; re-apply in cloud.  
- **Attachments** – Sync `bug-attachments/` & `project-attachments/` to object storage; update `mc_attachment_path`.  
- **Cron / Scheduled Jobs** – Recreate on-prem cron tasks in cloud scheduler.

---

## 2. Trial Terms & Conditions
| Item                | Value                      |
|---------------------|----------------------------|
| Duration            | 30 days (write access)     |
| Seats               | Up to 30 users             |
| Storage             | 5 GB total                 |
| Features            | Enterprise-level (DB import, unlimited API) |
| Limitations         | No SLA; non-extendable; write disables after trial |
| Export (post-trial) | DB dump or REST/SOAP API   |

---

## 3. Enterprise Subscription Highlights
- **Unlimited** seats & storage, 12-month term.  
- Dedicated container (4 vCPU / 32 GB RAM) with auto-scale.  
- 99.9 % uptime SLA; 24 × 7 support, 1-hour critical response.  
- Geo-redundant backups, point-in-time recovery.  
- Native SAML/OIDC, audit-trail exports, custom branding, white-label plugins.

---

## 4. Key Differences — Why On-Prem Is Outdated

| Area                 | On-Prem Reality (Aging)                                  | MantisHub Enterprise Advantage                     |
|----------------------|----------------------------------------------------------|----------------------------------------------------|
| **Upgrades & Patching** | Manual, weekend downtime, quarterly cadence            | Zero-downtime auto-updates (minor & major)         |
| **Infrastructure**   | Single VM, local RAID, no HA                             | HA container, auto-scales, geo-redundant           |
| **Storage**          | 80 % capacity, manual pruning                            | Unlimited object-store attachments                 |
| **Backups**          | Nightly `mysqldump` to local NAS                         | Geo-redundant, 5-min RPO, self-service restores    |
| **SSO**              | Legacy plugin, breaks on IdP updates                     | Native SAML + OIDC with role mapping               |
| **Compliance**       | Ad-hoc log retention, manual audit prep                  | SOC 2 Type II, GDPR, exportable audit trails       |
| **Plugin Lifecycle** | Manual pull & patch, downtime for updates                | Vendor-managed lifecycle, white-label support      |
| **Cost Predictability** | CapEx spikes for hardware refresh                      | Flat OpEx subscription, no hardware upkeep         |

---

## 5. Cross-Team Access & Compliance
- **Cybersecurity** – Admin login + API token; enable detailed logs; share TLS config for scans.  
- **Legal / Privacy** – Provide signed ToS, DPA, SOC 2, GDPR certs; review backup retention.  
- **Risk / Governance** – Verify encryption-at-rest, data residency (e.g., US-East1); log config changes.  
- **Stakeholder Comms** – Read-only dashboards, scheduled email reports, Slack notifications for “Legal Review” status.

---

## 6. Single Sign-On (SSO) Integration
1. **Upload** IdP metadata (SAML) **or** OIDC issuer/credentials.  
2. **Map** attributes: `email`, `displayName`.  
3. **Assign** groups → roles (e.g., “MantisAdmins” → administrator).  
4. **Test** provisioning and session timeout.

---

## 7. Customizations & Plugin Audit
- Export `mantis_custom_field_*`, `mantis_config_table`.  
- Re-enable supported plugins; plan replacements for unsupported ones.  
- Convert Drupal SQL calls to REST API endpoints.

---

## 8. Migration Mechanisms
| Path              | Description                                           | Tier Needed         |
|-------------------|-------------------------------------------------------|---------------------|
| DB-dump import    | Full schema + data via `mysqldump` into cloud DB       | Platinum / Enterprise |
| API / CSV import  | CSV/JSON → `mantisbt-importer` / REST API             | Gold +              |

---

## 9. Detailed Migration Tasks
1. **Issues** – Import `mantis_bug_*`; verify counts & sample histories.  
2. **Attachments** – Import file tables; upload via API; spot-check downloads.  
3. **Users / Roles** – Import user tables; validate SSO roles.  
4. **Custom Fields / Config** – Import; test issue creation.  
5. **Plugins** – Enable & test workflows.  
6. **Notifications** – Import email/webhook settings; send test events.

---

## 10. Operational Considerations
- **Backups** – Daily dumps to S3; quarterly restore test.  
- **Monitoring** – Prometheus metrics, Grafana alerts (CPU > 80 %, DB lag > 100 ms).  
- **Rollback** – Retain on-prem snapshot 7 days; scripted restore.  
- **Network Security** – Whitelist corp IPs; WAF rules.  
- **Training** – Update runbooks; 30-min user orientation; announce cut-over date.

---

## 11. Conclusion & Final Assessment
MantisHub Enterprise eliminates upgrade headaches, scaling limits, and compliance gaps in our aging on-prem setup while providing predictable OpEx, enterprise-grade SLAs, and unlimited growth headroom. Adopting it positions our team for faster delivery, stronger security, and lower total cost of ownership.