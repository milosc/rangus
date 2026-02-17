---
artifact_type: interview_analysis
interview_id: IVA-005
session_id: Session_2.1_Security
system_name: Ragus
stage: Discovery
created_at: 2026-02-16
version: 1.0.0
author: Discovery_InterviewAnalyst
status: completed
feedback_ref: FB-001
---

# Interview Analysis: Session 2.1 - Security & Operations Finalization

## Interview Metadata

| Field | Value |
|-------|-------|
| **Session ID** | Session_2.1_Security |
| **Focus** | Access Control, Data Retention, and Security Operations |
| **Duration** | Day 2, 02:00 PM – 03:00 PM |
| **Date** | [Interview Date from Source] |
| **Participants (Vendor)** | Sam (Security), Ken (DevOps) |
| **Participants (Client)** | Marcus (IT Manager), Dr. Halloway (GDPR) |

## Executive Summary

This final session established security operations requirements, including LDAP authentication, role-based access control (simplified to Clinical vs View-Only), ephemeral data storage (24-hour hard delete), and audit logging protocols. Key decisions include rejection of granular RBAC in favor of trust-based simplicity, physical security for kiosk mode, and 15-minute idle timeout with auto-save draft consideration.

**Primary Findings**:
- 14 client facts extracted
- 2 pain points identified (PP-5.1, PP-5.2)
- 2 user types profiled (IT Manager, Security Specialist)
- Simplified RBAC model (Clinical vs View-Only)
- Ephemeral data storage policy (24-hour hard delete)

---

## Pain Points Extracted

### PP-5.1: Data Liability Risk (Long-Term Storage)
- **Quote**: "You are not the medical record. You are a flow tool. Once the patient leaves the ER, hard delete from your system within 24 hours. Do not become a data liability." - Dr. Halloway [14:12]
- **Severity**: P0
- **Category**: Compliance & Security
- **Impact**: Long-term data storage creates GDPR liability; system must be ephemeral by design
- **User Type**: UT-2.2 (GDPR Lead - Dr. Halloway)
- **Trace**: CF-R-028

### PP-5.2: Session Timeout vs Data Loss
- **Quote**: "Ideally, auto-save draft? But if that's too complex, then yes, data lost is better than unauthorized access." - Marcus [14:49]
- **Severity**: P2
- **Category**: Usability vs Security Trade-off
- **Impact**: 15-minute idle timeout may cause data loss if form half-filled; security prioritized over convenience
- **User Type**: UT-3.1 (IT Manager - Marcus)
- **Trace**: CF-C-008

---

## Key Quotes

### CF-Q-017: Ephemeral Data Storage Mandate
> "You are not the medical record. You are a flow tool. Once the patient leaves the ER, hard delete from your system within 24 hours. Do not become a data liability." - Dr. Halloway [14:12]

**Analysis**: System positioned as transient workflow tool, not system of record. Data retention limited to active session + 24 hours for audit purposes only.

### CF-Q-018: Trust-Based RBAC Simplification
> "We trust our staff. Simplicity over granular restriction for this pilot. If someone messes up, we yell at them. We don't need code to prevent it." - Marcus [14:31]

**Analysis**: Rejects complex role hierarchies in favor of two-role model (Clinical vs View-Only). Human accountability over technical enforcement for pilot phase.

### CF-Q-019: Physical Kiosk Security
> "The USB ports are physically blocked with locks. And the account has no shell access. It strictly launches Chrome in Kiosk mode pointing to `localhost`." - Marcus [14:41]

**Analysis**: Multi-layer kiosk hardening: USB port locks + restricted OS account + Chrome kiosk mode. No software-only solution acceptable.

### CF-Q-020: Security Over Convenience (Idle Timeout)
> "Ideally, auto-save draft? But if that's too complex, then yes, data lost is better than unauthorized access." - Marcus [14:49]

**Analysis**: Security policy trumps user convenience. 15-minute idle timeout enforced even if it causes data loss.

---

## Workflow Observations

### Authentication Flow

```
Clinical Staff (Nurses, Doctors):
├── LDAP Authentication (Active Directory)
├── Role: "ER_Clinical_Staff" group
├── Permissions: Full CRUD (Create, Edit, Time Slot Assignment, Discharge)
└── Idle Timeout: 15 minutes → Redirect to login

Public Display (Kiosk):
├── Local OS account (restricted, no shell)
├── Role: "View Only"
├── Permissions: Read-only (public board data only)
├── Startup: Auto-launch Chrome Kiosk mode → https://localhost
└── Physical Security: USB ports locked, no keyboard access
```

### Data Lifecycle (Ephemeral Storage)

```
Patient Record Lifecycle:
├── 1. Created: Patient arrives at Intake
├── 2. Active: Patient in waiting room or treatment
├── 3. Discharged: Doctor marks disposition (Admitted/Discharged/LWBS/Transfer)
├── 4. Retention: Record kept for 24 hours post-discharge (audit trail)
└── 5. Deletion: Cron job at 04:00 AM hard deletes records >24h old

Cron Job Logic (04:00 AM daily):
DELETE FROM patients
WHERE status IN ('Discharged', 'Admitted', 'LWBS', 'Transfer')
AND discharge_timestamp < NOW() - INTERVAL '24 hours';

Exception: Do NOT delete active patients (status = "Waiting" or "In Treatment")
```

### Audit Logging (Action Trail)

```
Audit Log Entry:
{
  "timestamp": "2026-02-16T14:35:00Z",
  "user": "dr.evans",
  "action": "moved_patient",
  "patient_id": "JS-12",  // Pseudonymized ID
  "from_slot": "60m",
  "to_slot": "30m",
  "session_id": "abc123"
}

Retention: Audit logs kept for 30 days (separate from patient records)
Scope: Actions only (no patient PHI beyond pseudonym ID)
```

### RBAC Simplified Model

```
Role: Clinical (ER_Clinical_Staff AD group)
├── Permissions:
│   ├── Create patient records
│   ├── Edit intake/triage data
│   ├── Assign time slots (Doctor function)
│   ├── Mark dispositions (Discharged, LWBS, Transfer)
│   └── View internal nurse notes
└── Users: Jenny, Carol, Dr. Evans

Role: View Only (Kiosk)
├── Permissions:
│   └── Read public display data only (pseudonym ID, wait time category, status)
└── Users: Public Display TV
```

**Rejected Granular RBAC**:
- ❌ Separate Intake Nurse, Triage Nurse, Doctor roles
- ❌ Technical enforcement of "Nurse cannot assign time slots"
- ✅ Trust-based model: All clinical staff have full permissions

---

## Requirements Extracted

### CF-R-027: LDAP Authentication (Reconfirmed)
- **Source**: Sam [14:05], Marcus [14:06]
- **Requirement**: Nurses and doctors authenticate via LDAP (Active Directory)
- **Group**: "ER_Clinical_Staff" AD group
- **Kiosk**: Separate local account with no shell access, auto-launches Chrome Kiosk mode
- **Rationale**: Single sign-on for clinical staff; physical security for public display

### CF-R-043: Simplified RBAC (Two Roles)
- **Source**: Sam [14:22-14:27], Marcus [14:28-14:31]
- **Requirement**: Two-role model instead of granular RBAC
  - **Clinical**: Full CRUD permissions (Intake, Triage, Time Slots, Discharge)
  - **View Only**: Read-only public display data
- **Rejected**: Separate roles for Intake Nurse, Triage Nurse, Doctor
- **Rationale**: Trust-based model for pilot; human accountability over technical enforcement
- **Trace**: CF-Q-018

### CF-R-028: Ephemeral Data Storage (24-Hour Hard Delete)
- **Source**: Ken [14:10], Dr. Halloway [14:12], Sam [14:15]
- **Requirement**: Patient records hard deleted 24 hours after discharge
- **Cron Job**: Daily at 04:00 AM, deletes records with:
  - Status: "Discharged", "Admitted", "LWBS", "Transfer"
  - Timestamp: >24 hours old
- **Exception**: Do NOT delete active patients (status = "Waiting" or "In Treatment")
- **Rationale**: GDPR data minimization; system is not medical record, only flow tool
- **Trace**: PP-5.1

### CF-R-044: Cron Job Safety Logic
- **Source**: Marcus [14:18], Ken [14:19]
- **Requirement**: Deletion cron job logic:
  - `DELETE WHERE status IN ('Discharged', 'Admitted', 'LWBS', 'Transfer') AND timestamp > 12 hours`
- **Safety Check**: Do NOT delete patients who have been waiting since 10 PM (long waits)
- **Rationale**: Prevent accidental deletion of active long-wait patients

### CF-R-045: Audit Logging (Action Trail)
- **Source**: Ken [14:35], Dr. Halloway [14:36]
- **Requirement**: Log all actions (Create, Edit, Time Slot Assignment, Discharge)
- **Format**: `User X moved Patient Y to 30m` (pseudonymized patient ID: "JS-12")
- **Retention**: 30 days (separate from patient records, which are deleted in 24h)
- **Scope**: Actions only, no patient PHI beyond pseudonym ID
- **Rationale**: Audit trail for incident investigation without long-term patient data storage

### CF-R-046: Physical Kiosk Security
- **Source**: Ken [14:40], Marcus [14:41]
- **Requirement**: Public display TV security measures:
  - USB ports physically locked (prevent keyboard attachment)
  - Restricted OS account (no shell access)
  - Auto-launch Chrome Kiosk mode → `https://localhost` (full-screen, no UI chrome)
- **Rationale**: Multi-layer security to prevent unauthorized access via public display
- **Trace**: CF-Q-019

### CF-C-008: 15-Minute Idle Timeout (Session Expiry)
- **Source**: Sam [14:45], Marcus [14:46]
- **Constraint**: Clinical staff sessions expire after 15 minutes of inactivity
- **Action**: Redirect to login page (do NOT leave half-filled form open)
- **Trade-off**: Data loss vs unauthorized access
  - Ideal: Auto-save draft
  - Acceptable: Data lost if too complex to implement auto-save
- **Rationale**: Security policy mandates short idle timeout
- **Trace**: PP-5.2

### CF-R-047: Session Expiry Handling
- **Source**: Ken [14:48], Marcus [14:49]
- **Requirement**: If session expires with half-filled form:
  - **Preferred**: Auto-save draft to backend (restore on re-login)
  - **Acceptable**: Data lost (security > convenience)
- **Implementation**: Redirect to login with clear error message ("Session expired. Please log in again.")
- **Rationale**: Graceful degradation; no silent failures

### CF-R-048: VM Snapshot Backups (Hourly)
- **Source**: Sam [14:52], Marcus [14:53]
- **Requirement**: Infrastructure team snapshots VM every hour
- **Scope**: IT Ops responsibility (not vendor)
- **Vendor Requirement**: Application must be crash-consistent (database WAL)
- **Rationale**: Disaster recovery without long-term data retention

### CF-R-049: Database Crash Consistency (WAL)
- **Source**: Ken [14:55]
- **Requirement**: PostgreSQL Write-Ahead Logging (WAL) enabled for crash recovery
- **Outcome**: If VM restored from snapshot, database recovers to consistent state
- **Rationale**: Supports hourly VM snapshot strategy

### CF-C-010: Air-Gapped Bundle (Reconfirmed)
- **Source**: Sam [14:58], Marcus [14:59]
- **Constraint**: No external API calls (Google Fonts, CDNs, analytics)
- **Implementation**: Bundle all assets (fonts, JS libraries, CSS) in Docker image
- **Enforcement**: Firewall blocks external traffic; app fails visually if it tries to phone home
- **Rationale**: Security policy enforces air-gapped operation

---

## Role Profiles

### UT-3.1: IT Manager (Marcus - Client) - RECONFIRMED

**Responsibilities**:
- Security policy enforcement (LDAP, idle timeout, physical kiosk security)
- RBAC simplification decision (trust-based model)
- VM snapshot backups (hourly)

**Technical Proficiency**: Advanced
- Deep understanding of hospital security policies
- Balances security vs usability trade-offs

**Pain Points**:
- PP-5.2: Session timeout vs data loss (security prioritized)

**Quotes**:
- "For the nurses and doctors, yes. LDAP integration. For the TV display? It should be a kiosk mode account with no keyboard access."
- "We trust our staff. Simplicity over granular restriction for this pilot. If someone messes up, we yell at them."
- "The USB ports are physically blocked with locks. And the account has no shell access."
- "Yes, strict 15-minute idle timeout. Your app needs to handle the session expiry gracefully."
- "Ideally, auto-save draft? But if that's too complex, then yes, data lost is better than unauthorized access."
- "Snapshot the VM every hour. That's on us (Infrastructure). Your app just needs to be crash-consistent."
- "Correct. Air-gapped logic. Bundle everything. If it tries to phone home to `fonts.googleapis.com`, the firewall will drop it."

**Interface Requirements**:
- LDAP authentication module
- 15-minute idle timeout with graceful redirect
- Crash-consistent database (WAL)

---

### UT-5.1: Security Specialist (Sam - Vendor)

**Responsibilities**:
- RBAC design and simplification
- Audit logging requirements
- Physical kiosk security validation
- Session management policies

**Technical Proficiency**: Advanced
- Security architecture expertise
- Understands GDPR compliance requirements

**Pain Points**: None extracted (consultant/advocate role)

**Quotes**:
- "Authentication. Do we hook into your Active Directory?"
- "Let's talk about Role-Based Access Control (RBAC). Intake Nurse: Can Create, Edit. Triage Nurse: Can Edit (Vitals, ESI). Doctor: Can Edit (Time Slots, Discharge). Admin: Can Config?"
- "That simplifies things, but it means a junior nurse *could* mess with the board."
- "Audit Logging. Even if we don't keep patient data, we should log *actions*. 'User X moved Patient Y to 30m'."
- "Physical security. The server. Is it in a locked rack?"
- "Session management. If Dr. Evans leaves his Surface on the desk, does it auto-logout?"
- "Backups. We agreed on ephemeral data, but if the database corrupts at 2 PM, we need to restore the morning's intake."
- "Final check. No external APIs? No Google Fonts, no CDNs?"

**Interface Requirements**:
- Audit logging dashboard (for security review, not daily use)
- Session expiry handling with clear error messages

---

## Observations

### Trust-Based RBAC Philosophy

1. **Simplicity Over Enforcement**: Marcus explicitly chooses trust-based model over complex role hierarchies.
2. **Human Accountability**: "If someone messes up, we yell at them" reflects small-team culture where social accountability > technical controls.
3. **Pilot-Appropriate**: Granular RBAC deferred to production phase; pilot validates workflow, not permission boundaries.

### Ephemeral Data Design

1. **Not a System of Record**: Dr. Halloway's framing ("You are a flow tool") establishes system's transient nature.
2. **24-Hour Retention**: Balances audit trail needs (complaint resolution) with GDPR data minimization.
3. **Cron Job Safety**: Edge case handling (long-wait patients) shows attention to real-world complexities.

### Physical Security Layers

1. **USB Port Locks**: Hardware-level protection against keyboard attachment.
2. **Restricted OS Account**: Software-level constraint (no shell access).
3. **Kiosk Mode**: Application-level constraint (full-screen, no browser UI).
4. **Multi-Layer Defense**: No single point of failure; defense in depth.

### Session Timeout Trade-off

1. **Security > Convenience**: Marcus explicitly accepts data loss over unauthorized access risk.
2. **Auto-Save Draft Complexity**: Ideal solution acknowledged but not mandated; simplicity preferred.
3. **Graceful Degradation**: Clear error messaging more important than feature richness for pilot.

---

## Traceability Links

### Client Facts
- CF-Q-017: Ephemeral data storage mandate (Dr. Halloway)
- CF-Q-018: Trust-based RBAC simplification (Marcus)
- CF-Q-019: Physical kiosk security (Marcus)
- CF-Q-020: Security over convenience (Marcus)
- CF-C-008: 15-minute idle timeout
- CF-C-010: Air-gapped bundle (reconfirmed)
- CF-R-027: LDAP authentication (reconfirmed)
- CF-R-028: Ephemeral data storage (24-hour hard delete)
- CF-R-043: Simplified RBAC (two roles)
- CF-R-044: Cron job safety logic
- CF-R-045: Audit logging (action trail)
- CF-R-046: Physical kiosk security
- CF-R-047: Session expiry handling
- CF-R-048: VM snapshot backups (hourly)
- CF-R-049: Database crash consistency (WAL)

### Pain Points
- PP-5.1: Data liability risk (long-term storage)
- PP-5.2: Session timeout vs data loss

### User Types
- UT-3.1: IT Manager (Marcus)
- UT-5.1: Security Specialist (Sam)

---

## Next Steps

1. **LDAP Integration**: Active Directory authentication module with 15-minute idle timeout
2. **Ephemeral Data Cron Job**: 04:00 AM daily cleanup with safety logic
3. **Audit Logging**: Action trail with pseudonymized patient IDs (30-day retention)
4. **Kiosk Hardening**: Chrome Kiosk mode configuration + physical USB locks
5. **Session Expiry Testing**: Validate graceful redirect and error messaging
6. **Database WAL**: PostgreSQL Write-Ahead Logging configuration for crash consistency

---

## Version History

| Version | Date | Author | Changes | Feedback Ref |
|---------|------|--------|---------|--------------|
| 1.0.0 | 2026-02-16 | Discovery_InterviewAnalyst | Initial interview analysis | FB-001 |
