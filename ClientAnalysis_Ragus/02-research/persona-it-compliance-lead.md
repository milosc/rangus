---
document_id: PERSONA-Ragus-IT-COMPLIANCE-LEAD
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: discovery-personas
source_files:
  - 01-analysis/ANALYSIS_SUMMARY.md
  - traceability/user_types_registry.json
  - traceability/pain_points_registry.json
---

# Persona: IT & Compliance Lead (Marcus)

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Marcus Thompson (IT Manager + Compliance Liaison) |
| **Roles** | IT Manager / Operations + GDPR/HIPAA Compliance Officer |
| **Age** | 48 |
| **Experience** | 25 years in healthcare IT, 10 years in compliance |
| **Technical Proficiency** | Advanced |
| **Environment** | Server room, datacenter, compliance office |

## Profile

Marcus wears two hats: he manages the on-premise infrastructure (Ubuntu VMs, Docker, network VLANs) and ensures compliance with GDPR, HIPAA, and patient privacy regulations. He's responsible for system reliability, security, deployment, and defining privacy constraints like patient ID formats and data retention policies.

> "This system cannot depend on the internet. When a storm knocks out our connection, we still have 40 patients in the waiting room. The internal LAN must keep running."

Marcus enforces a strict on-premise-only architecture (no cloud dependencies), air-gapped deployment (bundle all assets, no CDNs), and 24-hour patient data deletion for GDPR compliance. He also manages the 2-week vendor access approval process, which makes rapid bug fixes challenging.

## Goals with Success Metrics

| Goal | Success Metric | Current State |
|------|----------------|---------------|
| Ensure system remains operational during internet outages | 99.9% uptime on internal LAN, zero data loss during outages | Cloud systems fail during storms (PP-3.1) |
| Maintain security compliance (GDPR/HIPAA) | Zero privacy violations, 100% audit compliance | Full patient names displayed (non-compliant) |
| Minimize vendor dependencies | Manual deployments, tarball delivery, no VPN required | 2-week VPN approval (PP-6.1) |
| Enable simple, reliable deployments | Deployment time <15 minutes, zero downtime | Manual Docker Compose, VM snapshots |

## Pain Points (Linked to Registry)

### P0 - Critical
- **[PP-2.1] Privacy violations with patient name displays**: Current systems display full patient names on public boards, creating GDPR and HIPAA violations. Non-negotiable compliance requirement.
- **[PP-3.1] Internet dependency creates system failure risk**: Cloud-based systems fail when internet connectivity is lost during storms or outages, but internal LAN remains operational. Cannot afford to lose waiting list data.

### P2 - Medium Priority
- **[PP-6.1] Vendor access requires 2-week approval**: External vendor VPN access requires lengthy 2-week approval process, preventing rapid bug fixes and updates. Must use manual tarball/patch delivery.
- **[PP-6.2] Session timeout causes data loss**: Strict 15-minute idle timeout for security compliance can cause loss of partially completed forms, forcing staff to re-enter data.

> "During Hurricane Season, we lose internet for 12-18 hours at a time. The ER doesn't stop. The system can't stop either."

## Daily Workflow

| Time | Activity | System Touchpoint | Pain Point |
|------|----------|-------------------|------------|
| 08:00 | Review system health (VM monitoring, logs) | SSH to Ubuntu VMs, check Docker containers | Hourly VM snapshots, audit logs |
| 09:00 | Process vendor access requests | 2-week VPN approval workflow | Delays bug fixes (PP-6.1) |
| 10:00 | Review compliance (GDPR/HIPAA audit) | Check public display logs, data retention (24-hour patient deletion) | Privacy violations (PP-2.1) |
| Random | Respond to system outage (internet down) | Verify internal LAN services remain operational | Cloud dependency failures (PP-3.1) |
| 15:00 | Manual deployment (new release) | Docker Compose down/up, tarball extraction | No automated CI/CD (vendor access restricted) |
| 17:00 | Configure LDAP/Active Directory | User authentication, role-based access (Clinical vs View-Only) | 15-minute idle timeout (PP-6.2) |

## Technical Context

- **Infrastructure**: On-premise Ubuntu 22.04 VMs (4 vCPUs, 16GB RAM)
- **Deployment**: Docker Compose, manual tarball delivery (no internet access)
- **Network**: VLAN segmentation, firewall rules, SSL-only (even internal LAN)
- **Authentication**: LDAP/Active Directory integration
- **Security**: Self-signed SSL certificates (pilot), 15-minute idle timeout, hourly VM snapshots
- **Data Retention**: 24-hour patient data deletion (GDPR), 30-day audit logs

## Jobs To Be Done (Preview)

When deploying and operating the system, Marcus needs to:
1. **Ensure system works offline** (no internet dependencies, bundle all assets)
2. **Enforce privacy compliance** (patient ID format: initials + day, max 8 characters, no names on public display)
3. **Deploy updates manually** (tarball delivery, Docker Compose restart)
4. **Manage LDAP authentication** (Active Directory integration, role-based access)
5. **Configure SSL/TLS** (self-signed certificates for pilot, public CA later)
6. **Audit data retention** (24-hour patient deletion, 30-day logs)

## Representative Quotes

> "If your system calls out to a CDN for a font or library, it's dead to me. Everything must be bundled in the tarball."

> "We have two types of users: Clinical (read/write) and View-Only (public display, reports). LDAP handles the authentication, the app handles the authorization."

> "The 15-minute idle timeout is non-negotiable. But if it breaks the UX, we need smart session management—like autosave drafts every 30 seconds."

## Design Implications

### Must Have
- ✅ On-premise deployment (Docker Compose, no cloud dependencies)
- ✅ Air-gapped build (bundle all assets, no CDN calls)
- ✅ LDAP/Active Directory authentication
- ✅ Role-based access control (Clinical vs View-Only)
- ✅ SSL-only (self-signed for pilot, public CA for production)
- ✅ 24-hour patient data deletion (GDPR compliance)
- ✅ 15-minute idle timeout (security policy)

### Should Have
- ⭐ Autosave drafts every 30 seconds (mitigate session timeout data loss)
- ⭐ Session warning at 14 minutes ("You will be logged out in 1 minute")
- ⭐ Hourly VM snapshots (backup/recovery)
- ⭐ Audit logging (30-day retention, anonymized patient IDs)

### Must NOT Have
- ❌ Internet dependencies (CDNs, external APIs, cloud services)
- ❌ Full patient names or medical details on public display
- ❌ Automated deployments requiring vendor VPN access

## Feature Priorities (Ranked)

1. **On-premise deployment** (Docker Compose, bundle all assets) - P0
2. **Privacy-compliant patient IDs** (initials + day, max 8 chars) - P0
3. **LDAP authentication** (Active Directory integration) - P1
4. **Role-based access control** (Clinical vs View-Only) - P1
5. **24-hour patient data deletion** (GDPR compliance) - P1
6. **Session timeout with autosave** (mitigate data loss) - P2
7. **SSL certificate management** (self-signed to public CA) - P2

## Success Indicators

- System remains operational during 12+ hour internet outages (99.9% LAN uptime)
- Zero GDPR/HIPAA violations detected in audits
- Deployment time <15 minutes (manual Docker Compose)
- Zero session timeout complaints from clinical staff (autosave enabled)

## Relationships

- **Reports To**: CIO / Hospital IT Director
- **Coordinates With**: Compliance Officer (GDPR/HIPAA), Vendor (tarball delivery), Clinical Staff (authentication, session timeout)
- **Serves**: All system users (infrastructure, security, compliance)

## Related Artifacts

- **User Types**: UT-2.1 (IT Manager / Operations), UT-2.2 (Compliance Officer)
- **Pain Points**: PP-2.1, PP-3.1, PP-6.1, PP-6.2
- **Source Facts**: CF-C-001, CF-C-004, CF-C-005, CF-C-006, CF-C-007, CF-C-008, CF-C-009, CF-O-003, CF-O-004, CF-O-005, CF-O-006, CF-O-007, CF-R-011, CF-R-013, CF-R-014, CF-R-016, CF-R-018, CF-R-027, CF-R-028, CF-R-029, CF-R-030, CF-R-031, CF-R-032, CF-R-033
- **Interview Sources**: Session_1.2_The_Privacy___Compliance_Barrier.md_, Session_1.3_Infrastrucrture_and_Interoperability.md, Session_2.1._Security___Operations_Finalization.md
