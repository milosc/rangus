---
artifact_type: interview_analysis
interview_id: IVA-003
session_id: Session_1.3
system_name: Ragus
stage: Discovery
created_at: 2026-02-16
version: 1.0.0
author: Discovery_InterviewAnalyst
status: completed
feedback_ref: FB-001
---

# Interview Analysis: Session 1.3 - Infrastructure & Interoperability

## Interview Metadata

| Field | Value |
|-------|-------|
| **Session ID** | Session_1.3 |
| **Focus** | Deployment, Network, and Interoperability |
| **Duration** | 01:00 PM – 02:00 PM |
| **Date** | [Interview Date from Source] |
| **Participants (Vendor)** | David (Lead Architect), Ken (DevOps), Raj (Interoperability) |
| **Participants (Client)** | Marcus (IT Manager), Sheila (IT Ops Manager) |

## Executive Summary

This session established the technical infrastructure constraints and deployment requirements for the on-premise pilot. Key decisions include Docker-based containerization, no EHR integration (standalone double-entry for pilot), SSL-only even on LAN, and air-gapped architecture (no external dependencies). The session also defined hardware specs, network segmentation, and rapid patching workflows.

**Primary Findings**:
- 12 client facts extracted
- 3 pain points identified (PP-3.1, PP-3.2, PP-6.1)
- 2 user types profiled (IT Manager, IT Ops Manager)
- On-premise deployment architecture established (Docker Compose on Kubernetes)
- Air-gapped requirement (no CDNs, bundled assets)

---

## Pain Points Extracted

### PP-3.1: Internet Dependency Risk
- **Quote**: "Our internet cuts out during storms, but the internal LAN stays up. We cannot lose the waiting list if AWS goes down." - Marcus [13:10]
- **Severity**: P0
- **Category**: Infrastructure Reliability
- **Impact**: Cloud-based solutions unacceptable; system must remain operational during internet outages
- **User Type**: UT-3.1 (IT Manager - Marcus)
- **Trace**: CF-C-004

### PP-3.2: Data Integrity (Double Entry Risk)
- **Quote**: "What if Jenny types 'Jonh Smith' in your app and 'John Smith' in Epic?" - Raj [13:35]
- **Severity**: P2
- **Category**: Data Quality
- **Impact**: Typos in standalone system won't match EHR records; accepted risk for pilot
- **User Type**: UT-3.3 (Interoperability Specialist - Raj)
- **Trace**: CF-C-005

### PP-6.1: Vendor VPN Access Blocked
- **Quote**: "No external VPN access for vendors without a 2-week approval process." - Sheila [13:43]
- **Severity**: P1
- **Category**: Deployment/Patching
- **Impact**: Critical bug fixes require manual tarball delivery and IT Ops application; no direct remote access
- **User Type**: UT-3.2 (IT Ops Manager - Sheila)
- **Trace**: CF-C-006

---

## Key Quotes

### CF-Q-008: On-Premise Non-Negotiable
> "Web-based is fine, but no cloud. This needs to run On-Premise. Our internet cuts out during storms, but the internal LAN stays up. We cannot lose the waiting list if AWS goes down." - Marcus [13:10]

**Analysis**: Establishes hard constraint for on-premise deployment. Reliability during internet outages is mission-critical; cloud-based solutions rejected outright.

### CF-Q-009: No EHR Integration for Pilot
> "For this pilot? No. It's standalone. We don't have time to approve an HL7 interface. Double entry for now. Nurse types name in your app, and separately in Epic." - Marcus [13:21]

**Analysis**: HL7/FHIR integration deferred to future phases. Pilot prioritizes speed over data integration; double-entry accepted as pilot-appropriate trade-off.

### CF-Q-010: Sub-Second Display Latency
> "Sub-second. If a patient sees the doctor click and the screen doesn't change, they start knocking on the glass." - Sheila [13:26]

**Analysis**: Reinforces real-time requirement from Session 1.1. Visual feedback must be immediate; WebSocket architecture mandatory.

### CF-Q-011: No External VPN Access
> "No external VPN access for vendors without a 2-week approval process. You will send me a new Docker image tarball, or a git patch. I will apply it." - Sheila [13:43]

**Analysis**: Security policy creates friction for rapid patching. Deployment workflow must be dead simple for IT Ops to apply without vendor support.

---

## Workflow Observations

### Deployment Architecture

```
Client Environment:
├── Kubernetes Cluster (Internal Apps)
│   ├── VLAN 10: Server Farm
│   │   └── VM: 4 vCPUs, 16GB RAM, Ubuntu 22.04 LTS
│   │       └── Docker Compose File
│   │           ├── Node.js/Python Backend (WebSocket server)
│   │           ├── PostgreSQL (Containerized)
│   │           └── React Frontend (Served via Backend)
│   ├── VLAN 40: Clinical & Kiosk
│   │   ├── Nurse Intake PCs (Desktop, 24" monitors)
│   │   ├── Dr. Evans Surface Tablet (Touch-friendly)
│   │   └── Waiting Room TV (Samsung Tizen + Chromebit)
│   │       └── Chrome Kiosk Mode → https://localhost (SSL)
│   └── Internal Firewall: Port 443 only (SSL-only, no port 80)

Time Synchronization:
└── Hypervisor NTP → Server System Time (NOT client browser time)

Patching Workflow:
1. Vendor sends Docker image tarball or git patch
2. IT Ops applies patch: `docker-compose down && docker-compose up -d`
3. No vendor VPN access (2-week approval required)
```

### Network Segmentation

- **VLAN 10 (Server Farm)**: Backend services
- **VLAN 40 (Clinical & Kiosk)**: Nurse PCs, Doctor tablets, Public display
- **Firewall Rules**: Port 443 only, SSL-only even on LAN
- **No External Access**: Air-gapped, no CDN dependencies

### Hardware Specifications

| Component | Specs | Notes |
|-----------|-------|-------|
| Server VM | 4 vCPUs, 16GB RAM, Ubuntu 22.04 | Sufficient for Node + Postgres |
| Database | PostgreSQL (containerized) | Preferred over SQLite for reliability |
| Display | Samsung TV (Tizen) + Chromebit | 1920x1080, Chrome Kiosk mode |
| Nurse PCs | Desktop, 24" monitors, Mouse/Keyboard | Standard workstations |
| Doctor Tablet | Microsoft Surface (touch-friendly) | Responsive design required |

---

## Requirements Extracted

### CF-C-004: On-Premise Deployment (HARD CONSTRAINT)
- **Source**: Marcus [13:10], Ken [13:12]
- **Constraint**: No cloud dependencies; system must run on internal LAN
- **Rationale**: Internet outages during storms; AWS downtime unacceptable
- **Implementation**: Docker Compose on Kubernetes, on-premise VM

### CF-C-005: No EHR Integration (Pilot Constraint)
- **Source**: Raj [13:15], Marcus [13:21]
- **Constraint**: Standalone system; no HL7/FHIR interface to Epic/Cerner
- **Trade-off**: Double data entry (nurse types in both systems)
- **Accepted Risk**: Data mismatch (typos) accepted for pilot phase
- **Rationale**: HL7 interface approval takes too long; pilot prioritizes speed

### CF-R-022: Sub-Second Display Latency (WebSocket)
- **Source**: David [13:20], Sheila [13:26]
- **Requirement**: When doctor updates time slot, TV display updates in sub-second latency
- **Implementation**: WebSocket server (Node.js), WebSocket client (React)
- **Rationale**: Patient behavior (knocking on glass) if delay is visible

### CF-R-025: Docker Compose Deployment
- **Source**: Ken [13:12], Sheila [13:13]
- **Requirement**: Deliver Docker Compose file with containerized Node + Postgres
- **Environment**: Kubernetes cluster, Ubuntu 22.04 LTS VM, 4 vCPUs, 16GB RAM
- **Rationale**: IT Ops prefers containerization; no bare-metal database installation

### CF-R-026: Postgres in Container (Not SQLite)
- **Source**: David [13:32], Sheila [13:33]
- **Requirement**: Use PostgreSQL (containerized) instead of SQLite
- **Rationale**: Reliability preference; containerized Postgres acceptable to IT Ops
- **Constraint**: No bare-metal database installation

### CF-C-007: SSL-Only on LAN (Port 443)
- **Source**: Marcus [13:47-13:50], Ken [13:48-13:51]
- **Constraint**: No unencrypted traffic (no port 80); port 443 only
- **Implementation**: Self-signed SSL certs for pilot
- **Distribution**: IT Ops pushes root CA to Chromebit and Nurse PCs via Group Policy
- **Rationale**: Security policy enforced even on internal LAN

### CF-R-027: LDAP/Active Directory Authentication
- **Source**: Sam [14:05], Marcus [14:06]
- **Requirement**: Nurses and doctors authenticate via LDAP (Active Directory integration)
- **Kiosk Mode**: Public display uses kiosk account with no keyboard access
- **Rationale**: Single sign-on (SSO) for clinical staff

### CF-C-006: No Vendor VPN Access
- **Source**: Ken [13:40], Sheila [13:43]
- **Constraint**: Vendor cannot VPN in; 2-week approval process
- **Patching Workflow**:
  1. Vendor sends Docker image tarball or git patch
  2. IT Ops applies: `docker-compose down && docker-compose up -d`
- **Rationale**: Security policy; minimize external access surface

### CF-R-030: Simple Deployment Script
- **Source**: Sheila [13:43]
- **Requirement**: Deployment script must be "dead simple"
- **Example**: `docker-compose down && docker-compose up -d`
- **Rationale**: IT Ops applies patches without vendor support; no complex procedures

### CF-R-031: Network Firewall Configuration
- **Source**: David [13:44], Marcus [13:46]
- **Requirement**: Vendor specifies which ports to open on internal firewall
- **Network**: VLAN 40 (Nurse PCs, Display) ↔ VLAN 10 (Server Farm)
- **Ports**: 443 only (HTTPS/WSS)
- **Rationale**: IT Ops configures firewall rules based on vendor specs

### CF-R-032: Responsive Design for Touch (Surface Tablet)
- **Source**: David [13:55], Sheila [13:56]
- **Requirement**: Doctor View must be touch-friendly and responsive (Microsoft Surface)
- **Constraint**: Desktops (24" monitors, mouse/keyboard) + tablet support
- **Rationale**: Dr. Evans carries Surface tablet; interface must work on both form factors

### CF-R-033: NTP Time Synchronization
- **Source**: Raj [13:58], Sheila [13:59]
- **Requirement**: Application uses server system time, NOT client browser time
- **Rationale**: Client clocks drift; hypervisor NTP ensures accurate timestamps
- **Implementation**: Backend generates all timestamps; frontend displays server time

### CF-C-009: Air-Gapped Architecture (No CDNs)
- **Source**: Sam [14:58], Marcus [14:59]
- **Constraint**: No external API calls (Google Fonts, CDNs, analytics)
- **Implementation**: Bundle all assets (fonts, JS libraries, CSS) in Docker image
- **Rationale**: Firewall blocks external traffic; if app phones home to `fonts.googleapis.com`, UI breaks
- **Enforcement**: Bundle verification during build process

---

## Role Profiles

### UT-3.1: IT Manager (Marcus - Client)

**Responsibilities**:
- Infrastructure approval (on-premise requirement)
- Network segmentation and firewall rules
- Security policy enforcement (SSL-only, LDAP)
- HL7 interface deferral decision

**Technical Proficiency**: Advanced
- Deep understanding of hospital IT infrastructure
- Network security and compliance background

**Pain Points**:
- PP-3.1: Internet dependency risk (storm outages)

**Quotes**:
- "Web-based is fine, but no cloud. This needs to run On-Premise. Our internet cuts out during storms, but the internal LAN stays up."
- "For this pilot? No. It's standalone. We don't have time to approve an HL7 interface. Double entry for now."
- "Yes, VLAN 40 is our 'Clinical & Kiosk' VLAN. They can talk to each other."
- "443 only. We don't allow unencrypted traffic, even on LAN."

**Interface Requirements**:
- Infrastructure monitoring dashboard (not part of pilot app)
- Firewall rule documentation

---

### UT-3.2: IT Ops Manager (Sheila - Client)

**Responsibilities**:
- VM provisioning (4 vCPUs, 16GB RAM)
- Docker Compose deployment and patching
- SSL certificate distribution (Group Policy)
- Display hardware management (Chromebit, smart TV)
- VM snapshot backups (hourly)

**Technical Proficiency**: Advanced
- DevOps expertise (containerization, Kubernetes)
- Prefers automation and simplicity

**Pain Points**:
- PP-6.1: Vendor VPN access blocked (2-week approval required)

**Quotes**:
- "Yes, we have a Kubernetes cluster for internal apps. But you need to handle the display hardware."
- "Sub-second. If a patient sees the doctor click and the screen doesn't change, they start knocking on the glass."
- "We prefer Postgres for reliability, but if you containerize it, I don't care."
- "No external VPN access for vendors without a 2-week approval process. You will send me a new Docker image tarball, or a git patch. I will apply it."
- "Keep the deployment script dead simple. `docker-compose down && docker-compose up -d`."
- "Snapshot the VM every hour. That's on us (Infrastructure). Your app just needs to be crash-consistent."

**Interface Requirements**:
- Simple deployment script (one-liner)
- Docker Compose file with clear documentation

---

### UT-3.3: Interoperability Specialist (Raj - Vendor)

**Responsibilities**:
- HL7/FHIR integration assessment
- Data mismatch risk analysis (double entry)

**Technical Proficiency**: Advanced
- Healthcare interoperability standards (HL7, FHIR)

**Pain Points**:
- PP-3.2: Data integrity risk (double-entry typos)

**Quotes**:
- "Do we need to pull patient demographics from your main EHR (Epic/Cerner)?"
- "Back to the 'Double Entry.' I'm worried about data mismatch. What if Jenny types 'Jonh Smith' in your app and 'John Smith' in Epic?"

**Interface Requirements**:
- Not applicable (no EHR integration for pilot)

---

## Observations

### Deployment Constraints

1. **On-Premise Mandate**: Hospital's internet reliability issues drive hard constraint for on-premise deployment. No cloud services accepted.
2. **Containerization Preferred**: IT Ops comfortable with Docker Compose; no bare-metal installations.
3. **Air-Gapped Architecture**: All assets must be bundled; no external dependencies (CDNs, Google Fonts).

### Security Requirements

1. **SSL-Only Even on LAN**: Unusual but enforced; requires self-signed cert management.
2. **LDAP Integration**: Single sign-on for clinical staff reduces credential sprawl.
3. **Kiosk Mode Hardening**: Public display uses locked-down account with no keyboard/shell access.

### Patching Friction

1. **No VPN Access**: Vendor cannot remotely apply patches; IT Ops becomes bottleneck.
2. **Simple Deployment Script**: One-liner deployment command reduces risk of IT Ops errors.
3. **Docker Image Tarball**: Offline delivery method for patches (no git pull from external repos).

### Accepted Trade-offs

1. **Double Entry Risk**: Typos in standalone system vs long HL7 approval process. Speed prioritized for pilot.
2. **SQLite vs Postgres**: Containerized Postgres chosen for reliability despite slightly higher resource usage.
3. **Self-Signed Certs**: Acceptable for pilot; production would require proper CA-signed certs.

---

## Traceability Links

### Client Facts
- CF-Q-008: On-premise non-negotiable (Marcus)
- CF-Q-009: No EHR integration for pilot (Marcus)
- CF-Q-010: Sub-second display latency (Sheila)
- CF-Q-011: No external VPN access (Sheila)
- CF-C-004: On-premise deployment constraint
- CF-C-005: No EHR integration (pilot constraint)
- CF-C-006: No vendor VPN access
- CF-C-007: SSL-only on LAN (port 443)
- CF-C-009: Air-gapped architecture (no CDNs)
- CF-R-022: Sub-second display latency (WebSocket)
- CF-R-025: Docker Compose deployment
- CF-R-026: Postgres in container (not SQLite)
- CF-R-027: LDAP/Active Directory authentication
- CF-R-030: Simple deployment script
- CF-R-031: Network firewall configuration
- CF-R-032: Responsive design for touch (Surface tablet)
- CF-R-033: NTP time synchronization

### Pain Points
- PP-3.1: Internet dependency risk
- PP-3.2: Data integrity (double entry risk)
- PP-6.1: Vendor VPN access blocked

### User Types
- UT-3.1: IT Manager (Marcus)
- UT-3.2: IT Ops Manager (Sheila)
- UT-3.3: Interoperability Specialist (Raj)

---

## Next Steps

1. **Docker Compose File**: Create containerized deployment with Node + Postgres + React
2. **SSL Certificate Generation**: Self-signed certs + root CA for Group Policy distribution
3. **LDAP Integration**: Active Directory authentication module
4. **Asset Bundling**: Verify no external CDN dependencies (Google Fonts, analytics)
5. **Deployment Documentation**: One-liner script with clear instructions for IT Ops

---

## Version History

| Version | Date | Author | Changes | Feedback Ref |
|---------|------|--------|---------|--------------|
| 1.0.0 | 2026-02-16 | Discovery_InterviewAnalyst | Initial interview analysis | FB-001 |
