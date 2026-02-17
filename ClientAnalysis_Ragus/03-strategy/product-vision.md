---
document_id: DISC-VISION-Ragus
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GenerateVision
source_files:
  - 02-research/persona-intake-nurse.md
  - 02-research/persona-triage-nurse.md
  - 02-research/persona-triage-doctor.md
  - 02-research/persona-patient-advocate.md
  - 02-research/persona-it-compliance-lead.md
  - 02-research/JOBS_TO_BE_DONE.md
  - traceability/pain_points_registry.json
---

# Product Vision - Ragus

## Vision Statement

> For **emergency room clinical staff and patients** who **need ultra-fast triage workflow with humane patient identification**, the **Ragus ER Triage System** is a **touchscreen-optimized clinical workflow platform** that **enables sub-30-second patient processing with glove-friendly interfaces and real-time status displays**. Unlike **traditional ER systems that prioritize data capture over speed and treat patients like numbers**, our product **prioritizes clinical safety through manual doctor control, preserves patient dignity with recognizable identifiers, and operates reliably on internal LAN during internet outages**.

## The Problem We're Solving

### Critical Pain Points (P0)

| ID | Pain Point | Impact | Users Affected |
|----|------------|--------|----------------|
| PP-1.1 | Slow patient intake during high-urgency situations | Dangerous delays in life-threatening situations, incomplete records | Intake nurses, triage nurses, urgent patients |
| PP-2.1 | Privacy violations with patient name displays | GDPR/HIPAA violations, legal liability, patient privacy breach | All patients, compliance team, hospital |
| PP-3.1 | Internet dependency creates system failure risk | Complete system outage, loss of patient queue data, manual paper fallback | All clinical staff, patients during outages |
| PP-5.1 | Countdown timers cause patient riots | Patient aggression, confrontations, unsafe environment, staff stress | All patients, clinical staff, security |
| PP-5.2 | Automated escalation ignores clinical judgment | Inappropriate prioritization, potential patient harm, overrides clinical expertise | Triage doctors, patients |

### Current State

Today's ER triage systems force clinical staff into impossible trade-offs:
- **Speed vs. Safety**: Nurses type frantically during trauma arrivals, creating dangerous delays and incomplete records
- **Privacy vs. Recognition**: Systems display full patient names (GDPR/HIPAA violations) or use dehumanizing ticket numbers that patients forget
- **Automation vs. Clinical Judgment**: Algorithms automatically escalate patients based on wait time alone, ignoring visual clinical indicators like profuse sweating or behavioral deterioration
- **Cloud Convenience vs. Reliability**: Internet outages during storms cause complete system failure, forcing fallback to paper-based chaos

Clinical staff work with gloved hands in high-pressure environments, yet systems provide tiny text links and mouse-centric interfaces. Float nurses arrive with zero training time. Patients and families experience anxiety from countdown timers that expire, leading to confrontations with staff.

## Our Solution

### Key Capabilities

| Capability | Pain Points Addressed | JTBDs Enabled |
|------------|----------------------|---------------|
| **Ultra-Fast Intake (Sub-30-Second Processing)** | PP-1.1 | JTBD-1.1, JTBD-1.4 |
| Tab-enter keyboard navigation, minimal required fields (Name, DOB, Complaint), giant "Emergency Bypass" button for trauma cases | Prevents dangerous delays during critical arrivals | Process urgent patients instantly, escalate trauma cases immediately |
| **Glove-Friendly Touchscreen Interface** | PP-1.3 | JTBD-1.2, JTBD-2.2, JTBD-3.7 |
| Large touch targets (60x60px minimum), one-click actions, tablet + desktop responsive design | Maintains infection control without workflow disruption | Work effectively with gloves, capture vitals quickly, seamless desktop/tablet workflow |
| **Privacy-Compliant Patient IDs (Initials + Day)** | PP-2.1, PP-2.2 | JTBD-4.1, JTBD-4.3, JTBD-4.5 |
| Patient identifiers in "LC-16" format (initials + day), no full names or medical details on public display | GDPR/HIPAA compliance while preserving human dignity | Patients recognize their ID, family tracking, privacy compliance |
| **Manual Doctor Control (Kanban Board)** | PP-5.2 | JTBD-3.1, JTBD-3.2 |
| Time-based Kanban columns (30m, 60m, 120m, Rest), drag-and-drop patient cards, zero automated escalation | Preserves clinical judgment over algorithmic assumptions | Maintain full manual control, visualize patient flow |
| **Real-Time WebSocket Updates (<1 Second)** | PP-3.2 | JTBD-3.4, JTBD-4.2 |
| Sub-second display latency when doctor assigns time slots, category-based wait times (not countdown timers) | Prevents patient confrontation, reduces anxiety | Update public display instantly, safe wait time communication |
| **On-Premise LAN Deployment** | PP-3.1 | JTBD-5.1 |
| Ubuntu VM + Docker deployment, zero cloud dependencies, tarball-based updates | System operates during internet outages, no data loss | Ensure system works during storms/outages |
| **Zero-Training Float Staff Onboarding** | PP-4.3 | JTBD-2.5 |
| Intuitive UI with logical workflow, discoverable actions, minimal cognitive load | Float nurses productive within 30 seconds | Onboard temporary staff without training time |
| **Dark Mode for Night Shifts** | PP-4.1, PP-4.2 | JTBD-1.6, JTBD-2.6, JTBD-4.4 |
| Automatic time-based or manual dark mode toggle for staff and public displays | Reduces eye strain and sensory overload at night | Work comfortably during night shifts, calming visual environment |
| **Visual Wait Time Alerts (No Automation)** | PP-3.2, PP-5.2 | JTBD-3.3 |
| Yellow border at 110% threshold, red border at 150%, manual re-evaluation only | Alerts doctor to escalating conditions without overriding clinical judgment | See real-time wait time alerts, preserve manual control |

### Value Proposition

Ragus eliminates the fundamental trade-offs that plague ER triage systems:
- **Speed AND Safety**: Process trauma patients in <30 seconds with complete data integrity
- **Privacy AND Recognition**: GDPR/HIPAA-compliant identifiers that patients can recognize ("LC-16" feels human, not like "cattle")
- **Automation AND Control**: Visual alerts inform doctor judgment without algorithmic overrides
- **Reliability AND Simplicity**: On-premise LAN deployment with 99.9% uptime, manual tarball updates without vendor VPN wait

**Unique Differentiator**: Clinical workflows designed **by** ER staff, **for** ER staff—glove-friendly, keyboard-first, zero-training, with manual control baked into every decision.

## Target Users

### Primary Personas

| Persona | Primary Need | Critical Job | Success Metric |
|---------|--------------|--------------|----------------|
| **Jenny Martinez** (Intake Nurse) | Process urgent patients in <30 seconds | JTBD-1.1: Process Urgent Patients Instantly | Intake time <30s for critical cases |
| **Carol Henderson** (Triage Nurse) | Identify next patient instantly without searching | JTBD-2.1: Identify Next Patient Instantly | Queue bottleneck eliminated (<5 min wait) |
| **Dr. Marcus Evans** (Triage Doctor) | Maintain full manual control over patient prioritization | JTBD-3.1: Maintain Full Manual Control | 100% manual time slot assignment, zero automated escalation |
| **Linda Chen** (Patient Rights Rep) | Ensure patients recognize their identifier on public display | JTBD-4.1: Ensure Patients Recognize Their ID | Patient satisfaction >4/5, zero "cattle" complaints |
| **Marcus Johnson** (IT/Compliance Lead) | Ensure system works during internet outages | JTBD-5.1: Ensure System Works During Internet Outages | 99.9% uptime on internal LAN, zero data loss |

### User Priorities

| Persona | Primary Need | Success Metric |
|---------|--------------|----------------|
| Intake Nurse | Ultra-fast processing (<30s for urgent patients) | Time from arrival to "Intake Complete" <30s |
| Triage Nurse | Auto-advance queue (next patient loads automatically) | Triage time <5 min per patient |
| Triage Doctor | Manual control over prioritization (no automation) | 100% manual time slot assignment |
| Patient Advocate | Privacy-compliant, recognizable patient IDs | GDPR/HIPAA compliance + patient satisfaction >4/5 |
| IT/Compliance Lead | On-premise LAN reliability during outages | 99.9% uptime, zero internet dependency |

## Success Criteria

### Business Outcomes

- **Reduced Patient Wait Times**: Intake-to-triage time drops from 10+ minutes to <5 minutes (50% reduction)
- **Compliance Achievement**: Zero GDPR/HIPAA violations detected in public display logs
- **System Reliability**: 99.9% uptime on internal LAN, zero data loss during internet outages
- **Staff Efficiency**: Float staff productive within 30 seconds (zero training time required)
- **Patient Satisfaction**: Patient experience rating >4/5 for wait time communication and identification

### User Outcomes

- **Clinical Staff Safety**: Zero infection control violations due to glove removal (glove-friendly UI)
- **Clinical Judgment Preserved**: 100% manual doctor control over patient prioritization (no automated escalation)
- **Patient Dignity**: Zero "cattle" complaints about dehumanizing numeric identifiers
- **Staff Comfort**: Eye strain rating <3/10 for night shift staff using dark mode
- **Reduced Confrontations**: Zero patient confrontations due to display lag or expired countdown timers

### Measurable KPIs

| KPI | Target | Current Baseline | Improvement |
|-----|--------|------------------|-------------|
| Intake Time (Urgent Patients) | <30 seconds | 60-90 seconds | 50-67% faster |
| Intake-to-Triage Wait Time | <5 minutes | 10+ minutes | 50% reduction |
| Triage Time per Patient | <5 minutes | 10+ minutes | 50% reduction |
| Display Update Latency | <1 second | 1-2 seconds | Real-time updates |
| System Uptime (LAN) | 99.9% | Unknown (cloud-dependent) | Storm-proof reliability |
| Float Staff Onboarding Time | <30 seconds | Requires buddy system | Zero training time |
| Patient Satisfaction (Wait Communication) | >4/5 | Unknown | Privacy + recognition |
| GDPR/HIPAA Violations | 0 | Multiple violations with full names | 100% compliance |

## Constraints & Assumptions

### Technical Constraints

- **On-Premise Only**: No cloud dependencies (CDNs, external APIs). All assets bundled in tarball.
- **LAN Deployment**: Ubuntu VM + Docker environment on internal hospital network.
- **Manual Updates**: Tarball delivery (no vendor VPN access). Updates require <15 minutes downtime.
- **LDAP Authentication**: Active Directory integration for role-based access (Clinical vs View-Only).
- **24-Hour Data Deletion**: GDPR compliance requires patient data deletion after 24 hours.
- **15-Minute Session Timeout**: Security compliance mandate (mitigated with autosave drafts).

### Usability Constraints

- **Zero Training Time**: Float staff must learn system in <30 seconds (no buddy system available).
- **Glove-Friendly**: Large touch targets (60x60px minimum), one-click actions, no tiny text links.
- **Tablet + Desktop**: Responsive design for Surface tablets and desktop monitors.
- **Keyboard-First**: Tab-enter navigation for high-speed data entry (never touch mouse).

### Clinical Constraints

- **100% Manual Control**: Zero automated escalation based on wait time. Doctor must manually assign all time slots.
- **No Countdown Timers**: Category-based wait times only ("30-minute wait" NOT "59:59" countdown).
- **Privacy-First Public Display**: No full names, no medical details, no GDPR/HIPAA violations.
- **Real-Time Updates**: Sub-second latency (<1s) when doctor updates patient status.

### Assumptions

- **Internet Outages Are Seasonal**: Storm-related, unpredictable frequency.
- **Clinical Staff Physical Constraints**: Gloves, sanitized hands, standing/sitting at desk, frequent interruptions.
- **Patient Volume**: 40-60 patients per shift during high-volume periods (flu season, weekends).
- **Float Staff Coverage**: Weekly rotation due to vacations, sick days, shift changes.
- **Night Shift Prevalence**: ~30% of operational hours (19:00-07:00).

---

**Document Status**: Complete
**Version**: 1.0.0
**Next Phase**: Generate Product Strategy and Roadmap

*Generated by Discovery Skills Framework v5.0*
