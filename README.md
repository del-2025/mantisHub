# MantisBT to MantisHub Enterprise
Migration Status and Architecture

## Where We Are

**Phase:** Technical validation and architecture review  
**Environment:** Trial only  
**Production Migration:** Not started

---

## Current Snapshot

| Area | Status |
|-----|-------|
| Technical feasibility | Complete |
| Architecture review | Complete |
| Security review | In progress |
| Legal and privacy review | In progress |
| Commercial review | Pending |
| Go / No-Go decision | Not decided |

---

## Work Completed

- Trial environment provisioned
- Core issue workflows validated
- REST API access validated
- Attachment upload and download validated
- Native SAML / OIDC flow reviewed
- Supported plugin set identified
- Architecture documented
- Migration boundaries identified
- Operational ownership defined

---

## Work In Progress

- Plugin parity inventory
- Mapping legacy SQL-based integrations to REST/API
- Security artifact review (SOC 2, GDPR, DPA)
- Contract and SLA review

---

## Not Started

- Production cutover planning
- Final migration sequencing
- User training and rollout
- On-prem decommissioning

---

## Known Constraints

- Direct database access is not available in MantisHub
- Unsupported legacy plugins exist
- Host-level cron jobs are not supported
- Full production load behavior not validated during trial

---

## Decision Gates

| Gate | Owner | Status |
|----|------|-------|
| Security sign-off | Cybersecurity | Pending |
| Legal approval | Legal | Pending |
| Commercial approval | Leadership | Pending |
| Go / No-Go | Executive | Not decided |

---

## Repository Structure

| Path | Description |
|----|------------|
| `/docs/architecture.md` | System architecture, data flow, migration boundaries |
| `/docs/migration-checklist.md` | Detailed migration checklist |
| `/docs/security-boundaries.md` | Security responsibility split |
| `/docs/operational-ownership.md` | Day-to-day ownership model |

---

## Notes

- This repository documents validation and planning only.
- No production data has been migrated.
- No irreversible actions have been taken.

---

_Last updated: 2026-02-10_

