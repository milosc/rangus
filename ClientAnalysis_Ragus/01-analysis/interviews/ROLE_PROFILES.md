---
artifact_type: role_synthesis
system_name: Ragus
stage: Discovery
created_at: 2026-02-16
version: 1.0.0
author: Discovery_InterviewAnalyst
status: completed
feedback_ref: FB-001
---

# Role Profiles: Ragus Emergency Room Triage System

## Executive Summary

This document consolidates all user types identified across 5 discovery interview sessions (Session 1.1, 1.2, 1.3, 2.1 Cross-Check, 2.1 Security). A total of 8 distinct user roles have been profiled, spanning clinical staff (intake, triage, doctor), compliance officers (data privacy, GDPR, patient rights), infrastructure managers (IT, IT Ops), and specialists (security, interoperability).

**User Types Summary**:
1. **UT-1.1**: Intake Nurse (Jenny) - Clinical
2. **UT-1.2**: Triage Nurse (Carol, Head Nurse) - Clinical
3. **UT-1.3**: Triage Doctor (Dr. Evans) - Clinical
4. **UT-2.1**: Data Privacy Officer (Elena) - Vendor
5. **UT-2.2**: GDPR Lead (Dr. Halloway) - Client
6. **UT-2.3**: Patient Rights Rep (Linda) - Client
7. **UT-3.1**: IT Manager (Marcus) - Client
8. **UT-3.2**: IT Ops Manager (Sheila) - Client
9. **UT-3.3**: Interoperability Specialist (Raj) - Vendor
10. **UT-4.1**: Float Nurse (Temporary Staff) - Clinical
11. **UT-5.1**: Security Specialist (Sam) - Vendor

---

## UT-1.1: Intake Nurse (Jenny)

### Role Summary

**Primary Function**: Initial patient registration at Intake Desk

**Responsibility**: Fast data capture to minimize patient wait time at entry point

**System Interaction**: Creates patient records (State 1: Intake Complete)

**Traceability**: Identified in Session 1.1 (Clinical Workflow)

---

### Detailed Responsibilities

1. **Patient Registration**:
   - Capture Name (First, Last)
   - Capture Date of Birth (DOB)
   - Capture Gender (M/F/Other) for disambiguation
   - Capture Chief Complaint (free text, minimal)
   - Capture Allergies (safety field)

2. **Privacy ID Generation**:
   - System auto-generates privacy-compliant ID (JS-12 format)
   - Resolve collisions if duplicate ID detected (append suffix: JS-12-A)

3. **Queue Management**:
   - Monitor pre-triage queue length
   - Communicate wait times to patients verbally (no system automation)

4. **Disposition Tracking**:
   - Mark patients as "Left Without Being Seen" (LWBS) if they leave before triage
   - Use disposition dropdown (Admitted, Discharged, LWBS, Transfer)

5. **Edge Case Handling**:
   - Manually override privacy ID for unidentified patients (e.g., "Trauma Alpha")

---

### Technical Proficiency

**Level**: Basic

**Comfort Zone**:
- Touchscreen input (prefers over mouse)
- Tab-enter keyboard shortcuts
- Minimal data entry workflows

**Avoids**:
- Excessive typing (CF-Q-001: "I don't want to type a novel")
- Complex forms with many fields
- Hidden menus or multi-step workflows

---

### Pain Points

#### PP-1.1: Slow Intake Workflow

**Quote**:
> "I need a screen there that is fast. I don't want to type a novel." - Jenny [Session 1.1, 09:04]

**Context**: Patients arrive clutching chest, in pain; speed is critical

**Impact**: Excessive data entry creates backlog at entry point, delays triage

**Severity**: P1

**Mitigation**: Minimal fields (CF-R-001) - Name, DOB, Chief Complaint, Allergies only

---

### Key Quotes

#### Quote 1: Fast Intake Requirement
> "Ideally, they stop at the Intake Desk first. But honestly? Half of them stumble in clutching their chest. If they can walk, they go to Intake. I need a screen there that is fast. I don't want to type a novel." - Jenny [Session 1.1, 09:04]

**Analysis**: Establishes critical requirement for minimal data entry. Only essential fields at intake.

---

#### Quote 2: LWBS Tracking
> "I need a way to mark them as 'Left Without Being Seen' (LWBS). This is a critical metric for us." - Jenny [Session 1.1, 09:23]

**Analysis**: LWBS is a hospital KPI; cannot simply delete patients who leave before treatment.

---

#### Quote 3: Real-Time Display Update
> "And once he clicks that, it needs to hit the TV screen in the Waiting Room immediately." - Jenny [Session 1.1, 09:20]

**Analysis**: Sub-second latency requirement for public display updates. WebSocket communication required.

---

### Interface Requirements

**Intake Screen Design**:
- Minimal fields (5 maximum): Name, DOB, Gender, Complaint, Allergies
- Touchscreen-friendly input
- Big buttons for gloved hands (≥44px touch targets)
- Tab-enter navigation for keyboard users
- Auto-generated privacy ID (JS-12) displayed after save
- "ADD PATIENT" and "SAVE" buttons prominently visible
- Dark mode support for night shift (CF-R-023)

**Disposition Tracking**:
- Dropdown: Admitted, Discharged, LWBS, Transfer
- Visible on patient list or dashboard (not buried in menus)

---

### Workflows Used

1. **Create Patient Record** (State 1: Intake Complete):
   - Open Intake form
   - Enter Name, DOB, Gender, Complaint, Allergies
   - Click "SAVE"
   - System generates privacy ID (JS-12)
   - Patient appears in Pre-Triage Queue

2. **Mark LWBS**:
   - Find patient in Pre-Triage Queue
   - Click "REMOVE" or "DISPOSITION"
   - Select "LWBS" from dropdown
   - Patient removed from public display but logged for metrics

---

### Traceability

**Client Facts**:
- CF-Q-001: Fast intake requirement
- CF-R-001: Minimal intake fields
- CF-R-002: Touchscreen or tab-enter navigation
- CF-R-008: LWBS tracking
- CF-R-010: Gender field for disambiguation
- CF-R-011: Privacy-compliant ID generation
- CF-R-020: Big, chunky buttons

**Pain Points**:
- PP-1.1: Slow intake workflow

**User Type ID**: UT-1.1

---

## UT-1.2: Triage Nurse (Carol, Head Nurse)

### Role Summary

**Primary Function**: Vital signs capture and Emergency Severity Index (ESI) assignment

**Responsibility**: Medical assessment in Triage Room; identifies workflow bottlenecks

**System Interaction**: Updates patient records with vitals and ESI level (State 2: Triage In-Progress)

**Traceability**: Identified in Session 1.1 (Clinical Workflow), Session 2.1 Cross-Check

---

### Detailed Responsibilities

1. **Vital Signs Capture**:
   - Blood Pressure (BP)
   - Heart Rate (HR)
   - Oxygen Saturation (O2)
   - Temperature (Temp)

2. **ESI Level Assignment**:
   - Assign Emergency Severity Index (1-5) based on clinical triage protocol
   - ESI 1: Immediate threat to life (resuscitation)
   - ESI 2: High risk (confused, lethargic, severe pain)
   - ESI 3: Moderate risk (stable vitals, standard resources)
   - ESI 4-5: Low risk (minor injuries, no resources needed)

3. **Triage Notes**:
   - Enter internal clinical observations (e.g., "Patient agitated", "Smells of alcohol")
   - Notes visible to doctor, NOT on public display (CF-R-036)

4. **Workflow Bottleneck Management**:
   - Prioritize ESI 1-2 patients
   - Monitor pre-triage queue length
   - Communicate with Intake Nurse (Jenny) about capacity

5. **Float Nurse Onboarding**:
   - Train temporary staff during vacations (zero-training constraint)
   - Validate that UI is self-explanatory for float nurses (PP-4.3)

---

### Technical Proficiency

**Level**: Basic

**Comfort Zone**:
- Gloved hands (requires large touch targets)
- High contrast UI (low-light conditions during night shift)
- Simple, linear workflows

**Avoids**:
- Tiny text links or buttons
- Complex multi-step forms
- Mouse-driven interfaces (prefers touchscreen or big buttons)

---

### Pain Points

#### PP-1.2: Triage Bottleneck

**Quote**:
> "This is where the bottleneck happens. Jenny captures them. Then they sit for maybe 10 minutes before I call them into the Triage Room for vitals." - Carol [Session 1.1, 09:07]

**Context**: Single triage nurse processing multiple patients; 10-minute wait between intake and triage

**Impact**: Patient anxiety increases; perception of long wait times even if total time is acceptable

**Severity**: P0

**Mitigation**: System provides queue visibility but cannot solve staffing constraint

---

#### PP-1.3: Gloved Hands UX Challenge

**Quote**:
> "My hands are often gloved, or I've just sanitized them. Tiny text links are a nightmare. I need big, chunky buttons." - Carol [Session 1.1, 09:28]

**Context**: Infection control protocols require gloves or frequent hand sanitization

**Impact**: Small UI elements difficult to interact with; reduces data entry speed

**Severity**: P1

**Mitigation**: Touch targets ≥44x44px (CF-R-020); big buttons for all actions

---

#### PP-4.3: Zero-Training Constraint

**Quote**:
> "Zero. It needs to be intuitive. If Jenny takes a vacation and we have a float nurse, she needs to figure it out in 30 seconds. Big labels. 'ADD PATIENT.' 'SAVE.' No hidden menus." - Carol [Session 2.1 Cross-Check, 10:49]

**Context**: Float nurses fill in during vacations; no training time available

**Impact**: Complex UI blocks temporary staff; causes workflow disruptions

**Severity**: P1

**Mitigation**: Self-explanatory UI with big labels (CF-R-040); no hidden menus

---

#### PP-4.4: Night Shift Eye Strain

**Quote**:
> "Bright white screens hurt [at night]." - Carol [Session 2.1 Cross-Check, 10:31]

**Context**: ER operates 24/7; night shift requires low-light UI

**Impact**: Eye strain during night shifts; reduces nurse productivity

**Severity**: P2

**Mitigation**: Dark mode support for all nurse interfaces (CF-R-023)

---

### Key Quotes

#### Quote 1: Triage Bottleneck
> "This is where the bottleneck happens. Jenny captures them. Then they sit for maybe 10 minutes before I call them into the Triage Room for vitals." - Carol [Session 1.1, 09:07]

**Analysis**: Identifies primary workflow bottleneck between State 1 and State 2.

---

#### Quote 2: Gloved Hands UX
> "My hands are often gloved, or I've just sanitized them. Tiny text links are a nightmare. I need big, chunky buttons." - Carol [Session 1.1, 09:28]

**Analysis**: Establishes critical UX requirement for touchscreen-friendly design with large touch targets.

---

#### Quote 3: Zero-Training Mandate
> "Zero. It needs to be intuitive. If Jenny takes a vacation and we have a float nurse, she needs to figure it out in 30 seconds. Big labels. 'ADD PATIENT.' 'SAVE.' No hidden menus." - Carol [Session 2.1 Cross-Check, 10:49]

**Analysis**: Defines hard constraint for self-explanatory UI; no training budget for temporary staff.

---

#### Quote 4: Dark Mode Requirement
> "And the Intake View needs Dark Mode. We work nights. Bright white screens hurt." - Carol [Session 2.1 Cross-Check, 10:31]

**Analysis**: Night shift ergonomics requirement; extends dark mode to all nurse interfaces.

---

### Interface Requirements

**Triage Screen Design**:
- Big, chunky buttons: "START TRIAGE", "SAVE", "COMPLETE TRIAGE" (≥44px touch targets)
- High contrast colors (low-light conditions)
- Dark mode toggle (CF-R-023)
- Visual alerts for ESI level escalations (red, pulsing)
- Minimal text entry (vitals are numeric, ESI is dropdown)

**Vitals Entry**:
- Numeric input fields (BP, HR, O2, Temp)
- Large touch targets for gloved hands
- Tab-enter navigation

**ESI Level Dropdown**:
- Large dropdown with clear labels (1-5)
- Color-coded (ESI 1-2 red, ESI 3 yellow, ESI 4-5 green)

**Triage Notes**:
- Free text field (internal only)
- Auto-save draft (if session timeout occurs)

---

### Workflows Used

1. **Start Triage** (State 2: Triage In-Progress):
   - Select patient from Pre-Triage Queue
   - Click "START TRIAGE"
   - Enter Vitals (BP, HR, O2, Temp)
   - Select ESI Level (1-5)
   - Enter Triage Notes (internal only)
   - Click "COMPLETE TRIAGE"
   - Patient moves to "Triaged" queue (visible to doctor)

2. **Monitor Queue**:
   - View Pre-Triage Queue length
   - Prioritize ESI 1-2 patients visually (red alerts)

---

### Traceability

**Client Facts**:
- CF-O-001: Bottleneck observation
- CF-R-003: Pre-triage state support
- CF-R-004: ESI level capture
- CF-R-020: Big, chunky buttons
- CF-R-023: Dark mode for intake/triage view
- CF-R-036: Internal-only nurse notes
- CF-R-040: Zero-training UX design

**Pain Points**:
- PP-1.2: Triage bottleneck
- PP-1.3: Gloved hands UX challenge
- PP-4.3: Zero-training constraint
- PP-4.4: Night shift eye strain

**User Type ID**: UT-1.2

---

## UT-1.3: Triage Doctor (Dr. Evans)

### Role Summary

**Primary Function**: "Fast Scan" review of triaged patients and manual time slot assignment

**Responsibility**: Clinical judgment for patient prioritization; bulk re-categorization when ER capacity changes

**System Interaction**: Reviews patient cards (State 3: Triaged) and assigns time slots (State 4: Time Slot Assigned)

**Traceability**: Identified in Session 1.1 (Clinical Workflow), Session 2.1 Cross-Check

---

### Detailed Responsibilities

1. **Fast Scan Review**:
   - View list of triaged patients on dashboard
   - Scan patient cards: age, chief complaint, vital signs, ESI level, nurse notes
   - Mentally assess urgency based on clinical judgment

2. **Manual Time Slot Assignment**:
   - Assign time category: Immediate, 30m, 60m, 120m, Standard Wait
   - NO automated time calculation (CF-R-005, CF-Q-002)
   - Decision based on: vitals, complaint, current ER load, observed patient distress

3. **Kanban Board Management**:
   - Drag-and-drop patient tiles between time slot columns (CF-R-009)
   - Bulk re-categorization when ER capacity changes (e.g., 5 ambulances arrive → drag existing "30m" patients to "60m")

4. **Progressive Alert Monitoring**:
   - Monitor yellow/red alerts for patients exceeding assigned wait times
   - Yellow: 110% of assigned wait time (e.g., 70 min for 60m slot)
   - Red: 150% of assigned wait time (e.g., 90 min for 60m slot)

5. **Behavioral Risk Flagging**:
   - Toggle "Behavioral Risk" checkbox for aggressive or agitated patients (CF-R-029)
   - Internal only (not visible on public display)
   - Use case: Prevent sending student nurses alone to aggressive patients

---

### Technical Proficiency

**Level**: Basic

**Comfort Zone**:
- Visual dashboards (prefers Kanban board over text lists)
- One-click actions (no right-click, no modifier keys)
- Touch-friendly interfaces (uses Microsoft Surface tablet)

**Avoids**:
- Complex data entry forms
- Right-click context menus
- Shift/Ctrl modifier keys
- Automated recommendations (trusts own judgment over algorithms)

---

### Pain Points

#### PP-4.2: Auto-Escalation Safety Risk

**Quote**:
> "Just because they waited doesn't mean they are dying." - Dr. Evans [Session 2.1 Cross-Check, 10:07]

**Context**: Elapsed wait time does not correlate to clinical urgency; automated escalation would misrepresent severity

**Impact**: Automated time slot escalation (e.g., 60m → 30m after 70 minutes) could create false sense of urgency or mislead clinical staff

**Severity**: P0

**Mitigation**: NO automated time slot changes (CF-R-035); visual alerts on doctor dashboard only

---

#### PP-5.2: Aggressive Patient Safety

**Quote**:
> "Occasionally we get aggressive patients. I want a checkbox or a toggle on the card that says 'Behavioral Risk.'" - Dr. Evans [Session 1.1, 09:52]

**Context**: Staff safety risk if behavioral patients not flagged

**Impact**: Student nurses or junior staff may be sent alone to aggressive patients without warning

**Severity**: P2

**Mitigation**: Behavioral risk flag (CF-R-029) visible to clinical staff only (internal only)

---

### Key Quotes

#### Quote 1: Manual Clinical Judgment (No Automation)
> "Absolutely not. Algorithms don't see that a guy is sweating profusely. I set the time manually based on the load." - Dr. Evans [Session 1.1, 09:16]

**Analysis**: Explicit rejection of automated time calculation. System must support manual time slot assignment.

---

#### Quote 2: Kanban Board Request
> "A Kanban view would be perfect. Columns for 'To Be Triaged,' '30m,' '60m,' '120m,' 'Rest.' Let me drag tiles." - Dr. Evans [Session 1.1, 09:39]

**Analysis**: Drag-and-drop interface enables bulk re-categorization when ER capacity changes.

---

#### Quote 3: Behavioral Risk Flag
> "Occasionally we get aggressive patients. I want a checkbox or a toggle on the card that says 'Behavioral Risk.'" - Dr. Evans [Session 1.1, 09:52]

**Analysis**: Staff safety requirement; internal-only flag to prevent sending junior staff alone to aggressive patients.

---

#### Quote 4: No Auto-Escalation
> "Just because they waited doesn't mean they are dying. However, I want a visual cue for me. If they sit in '60 min' bucket for 90 minutes, turn their row red on my dashboard. But do NOT change the public board automatically." - Dr. Evans [Session 2.1 Cross-Check, 10:07-10:09]

**Analysis**: Confirms rejection of automated clinical decision-making. System provides alerts to doctor but never changes patient status autonomously.

---

#### Quote 5: Progressive Alert Thresholds
> "Exactly. It helps me triage my own attention. I look for the red bars." - Dr. Evans [Session 2.1 Cross-Check, 10:38]

**Analysis**: Visual scan optimization for busy ER environment; color-coded progressive alerts (yellow at 110%, red at 150%).

---

#### Quote 6: One-Click Actions
> "If I have to right-click or use a modifier key, I won't use it. Left click / Touch only." - Dr. Evans [Session 2.1 Cross-Check, 10:52]

**Analysis**: Doctor mobility (Surface tablet) requires one-click actions; no complex interactions.

---

### Interface Requirements

**Doctor Dashboard Design**:
- Kanban board with drag-and-drop (CF-R-009)
- Columns: "To Be Triaged", "Immediate", "30m", "60m", "120m", "Standard Wait"
- Patient cards show: Privacy ID (JS-12), Age, Chief Complaint, Vitals, ESI Level, Nurse Notes, Behavioral Risk Flag
- One-click time slot buttons (Immediate, 30m, 60m, 120m, Standard Wait) (CF-R-006)
- Progressive alerts (yellow background at 110%, red at 150%) (CF-M-001)
- Visual alerts for ESI escalations (red, pulsing)
- Touch-friendly (Surface tablet support) (CF-R-032)
- No right-click or modifier keys (CF-R-041)
- Color-blind accessible (icons + text, not color alone) (CF-R-042)

**Patient Card Layout**:
```
┌─────────────────────────────┐
│ JS-12   Age: 45   ESI: 2    │ [Behavioral Risk: ⚠️]
│ Chief Complaint: Chest Pain │
│ BP: 150/90  HR: 95  O2: 94% │
│ Temp: 37.2°C                │
│ Notes: "Patient sweating    │
│        profusely"            │
│ [Immediate] [30m] [60m]     │
│ [120m] [Standard Wait]      │
└─────────────────────────────┘
```

---

### Workflows Used

1. **Fast Scan Review** (State 3: Triaged):
   - Open Doctor Dashboard
   - View "To Be Triaged" column (Kanban board)
   - Scan patient cards visually (age, complaint, vitals, ESI, notes)
   - Click time slot button or drag tile to column
   - Patient moves to assigned time slot column
   - Public display updates in sub-second latency (WebSocket)

2. **Bulk Re-Categorization**:
   - ER suddenly gets 5 ambulance arrivals (high acuity)
   - Drag multiple patient tiles from "30m" column to "60m" column
   - All affected patients' public display status updates automatically

3. **Progressive Alert Monitoring**:
   - Patient "JS-12" assigned to "60m" slot
   - After 70 minutes (110% threshold), row background turns YELLOW
   - After 90 minutes (150% threshold), row background turns RED
   - Doctor manually re-categorizes patient (drag to "30m" column) or calls patient immediately

4. **Behavioral Risk Flagging**:
   - Review patient card
   - Toggle "Behavioral Risk" checkbox
   - Flag visible to clinical staff only (not on public display)

---

### Traceability

**Client Facts**:
- CF-Q-002: Manual clinical judgment (no automation)
- CF-R-005: Manual time slot assignment
- CF-R-006: Doctor dashboard requirements
- CF-R-009: Kanban board interface
- CF-R-029: Behavioral risk flag
- CF-R-032: Responsive design for touch (Surface tablet)
- CF-R-035: No auto-escalation logic
- CF-R-041: One-click actions (no right-click)
- CF-R-042: Color-blind accessible alerts
- CF-M-001: Progressive alert thresholds (configurable)
- CF-M-002: Configurable alert formula

**Pain Points**:
- PP-4.2: Auto-escalation safety risk
- PP-5.2: Aggressive patient safety

**User Type ID**: UT-1.3

---

## UT-2.1: Data Privacy Officer (Elena - Vendor)

### Role Summary

**Primary Function**: GDPR/HIPAA compliance enforcement and privacy-by-design validation

**Responsibility**: Privacy-compliant ID design, data retention policy definition, audit trail requirements

**System Interaction**: Compliance audit dashboard (for validation, not daily use)

**Traceability**: Identified in Session 1.2 (Privacy & Compliance)

---

### Detailed Responsibilities

1. **GDPR/HIPAA Compliance Enforcement**:
   - Validate that NO PII (full names, medical conditions) displayed on public board (CF-C-001)
   - Review privacy-compliant ID format (JS-12) for re-identification risk
   - Assess small-town re-identification scenarios

2. **Privacy-by-Design System Validation**:
   - Pseudonymized patient IDs (hashed or JS-12 format)
   - Internal-only nurse notes (not on public API)
   - Safe status message enum (no psychiatric or sensitive dispositions)

3. **Data Retention Policy Definition**:
   - Ephemeral data storage (24-hour retention) (CF-R-028)
   - Audit logs (30-day retention) (CF-R-045)
   - Data minimization (GDPR Article 5)

4. **Audit Trail Requirements**:
   - Log all actions (Create, Edit, Time Slot Assignment, Discharge)
   - Pseudonymized patient IDs only (no PHI beyond pseudonym)
   - 30-day retention for incident investigation

---

### Technical Proficiency

**Level**: Advanced

**Expertise**:
- GDPR/HIPAA regulatory frameworks
- Privacy-by-design principles
- Data minimization strategies
- Pseudonymization techniques

---

### Pain Points

None extracted (advocate/enforcer role, not end user)

---

### Key Quotes

#### Quote 1: Privacy Non-Negotiable
> "Under GDPR and HIPAA, we cannot display names. 'John Smith: 30 minutes' is a violation. This is non-negotiable." - Elena [Session 1.2, 11:05]

**Analysis**: Establishes absolute requirement for privacy-compliant patient identification. No exceptions.

---

#### Quote 2: Pseudonym Proposal
> "Proposal: When Jenny does the intake, the system assigns a pseudonym or a 'Call Name' that is printed on a wristband?" - Elena [Session 1.2, 11:10]

**Analysis**: Initial proposal for privacy ID format; led to Initials + Day format (JS-12).

---

#### Quote 3: Data Minimization
> "Data minimization. How long do we keep the logs?" - Elena [Session 1.2, 11:50]

**Analysis**: GDPR Article 5 requirement; balances audit trail needs with data minimization principle.

---

### Interface Requirements

**Compliance Audit Dashboard** (for validation, not daily use):
- Privacy risk assessment report (pre-deployment)
- Sensitive data exposure risks (PII, medical conditions)
- Audit logs with pseudonymized IDs (hashed or JS-12 format)
- Data retention compliance (24-hour patient records, 30-day audit logs)

---

### Traceability

**Client Facts**:
- CF-Q-004: Privacy non-negotiable
- CF-C-001: GDPR/HIPAA privacy compliance (HARD CONSTRAINT)
- CF-R-011: Privacy-compliant patient ID format
- CF-R-019: Data retention policy (30 days for audit logs)
- CF-R-028: Ephemeral data storage (24-hour hard delete)
- CF-R-045: Audit logging (action trail)

**Pain Points**: None (advocate/enforcer role)

**User Type ID**: UT-2.1

---

## UT-2.2: GDPR Lead (Dr. Halloway - Client)

### Role Summary

**Primary Function**: GDPR compliance veto authority and privacy risk assessment

**Responsibility**: Small-town re-identification risk analysis, data retention policy approval, status message safety validation

**System Interaction**: Privacy audit report (pre-deployment validation)

**Traceability**: Identified in Session 1.2 (Privacy & Compliance), Session 2.1 Security

---

### Detailed Responsibilities

1. **GDPR Compliance Veto Authority**:
   - Reject any design that violates GDPR/HIPAA
   - Final approval on privacy-compliant ID format (JS-12)
   - Validate safe status message enum

2. **Privacy Risk Assessment (Small-Town Context)**:
   - Evaluate re-identification risk in small communities
   - Reject "First + Initial" format (e.g., "John S.") due to social context enabling re-identification

3. **Data Retention Policy Approval**:
   - Approve 24-hour ephemeral data retention (CF-R-028)
   - Approve 30-day audit log retention (CF-R-045)
   - Mandate "You are a flow tool, not a medical record" (CF-Q-017)

4. **Status Message Safety Validation**:
   - Approve safe status message enum (CF-R-017)
   - Prohibit psychiatric or sensitive dispositions ("Transfer to Psych")

5. **Collision Detection Validation**:
   - Approve collision handling logic (suffix: JS-12-A, JS-12-B)
   - Validate edge case scenarios (unidentified patients)

---

### Technical Proficiency

**Level**: Intermediate

**Expertise**:
- Legal/compliance background
- GDPR/HIPAA implications
- Re-identification risk analysis

---

### Pain Points

#### PP-2.2: Privacy vs Usability Conflict

**Quote**:
> "Too risky. In a small town, everyone knows 'John S.' with a broken arm is John Smith the baker." - Dr. Halloway [Session 1.2, 11:11]

**Context**: Traditional partial identifiers (First + Initial) fail in small communities where social context enables re-identification

**Impact**: Privacy violation risk; GDPR Article 4(1) defines re-identifiable data as PII

**Severity**: P0

**Mitigation**: Initials + Day format (JS-12) obscure enough to prevent casual re-identification

---

### Key Quotes

#### Quote 1: Privacy Non-Negotiable (Confirmation)
> "Correct. This is non-negotiable." - Dr. Halloway [Session 1.2, 11:06]

**Analysis**: Confirms Elena's statement; GDPR/HIPAA compliance is absolute requirement.

---

#### Quote 2: Small-Town Re-Identification Risk
> "Too risky. In a small town, everyone knows 'John S.' with a broken arm is John Smith the baker." - Dr. Halloway [Session 1.2, 11:11]

**Analysis**: Rejects "First + Initial" format due to small community re-identification risk.

---

#### Quote 3: Collision Detection Requirement
> "It's rare, but statistically possible. The system needs to detect that [collision]." - Dr. Halloway [Session 1.2, 11:26]

**Analysis**: Validates need for collision detection logic (CF-R-014).

---

#### Quote 4: Status Message Safety
> "Do NOT show 'Transfer to Psych.'" - Dr. Halloway [Session 1.2, 11:41]

**Analysis**: Prohibits psychiatric or sensitive dispositions on public display (HIPAA compliance).

---

#### Quote 5: Ephemeral Data Mandate
> "You are not the medical record. You are a flow tool. Once the patient leaves the ER, hard delete from your system within 24 hours. Do not become a data liability." - Dr. Halloway [Session 2.1 Security, 14:12]

**Analysis**: Establishes system's ephemeral nature; data retention limited to active session + 24 hours.

---

### Interface Requirements

**Privacy Audit Report** (pre-deployment validation):
- Privacy risk assessment (PII exposure, re-identification scenarios)
- Compliance dashboard showing sensitive data exposure risks
- Collision detection logic validation
- Data retention compliance (24-hour patient records, 30-day audit logs)

---

### Traceability

**Client Facts**:
- CF-Q-004: Privacy non-negotiable (confirmation)
- CF-Q-006: Small-town re-identification risk
- CF-Q-007: Status message safety
- CF-Q-017: Ephemeral data storage mandate
- CF-C-001: GDPR/HIPAA compliance constraint
- CF-R-011: Privacy-compliant ID format (JS-12)
- CF-R-014: Collision detection logic
- CF-R-017: Safe status message enum
- CF-R-019: Data retention policy (30 days for audit logs)
- CF-R-028: Ephemeral data storage (24-hour hard delete)

**Pain Points**:
- PP-2.2: Privacy vs usability conflict
- PP-5.1: Data liability risk (long-term storage)

**User Type ID**: UT-2.2

---

## UT-2.3: Patient Rights Rep (Linda)

### Role Summary

**Primary Function**: Patient advocacy (dignity, anxiety reduction, accessibility)

**Responsibility**: Display clarity validation, family member experience (reassurance), accessibility requirements

**System Interaction**: Public display (waiting room) validation

**Traceability**: Identified in Session 1.2 (Privacy & Compliance), Session 2.1 Cross-Check

---

### Detailed Responsibilities

1. **Patient Advocacy**:
   - Ensure patient dignity (no "cattle" feeling from ticket numbers)
   - Reduce patient anxiety (no countdown timers, category display only)
   - Validate display clarity (readability, high contrast)

2. **Display Clarity Validation**:
   - High readability (large fonts, high contrast)
   - Two-section layout (waiting queue + in-treatment list) (CF-R-018)
   - Visual update notifications (blink/highlight when status changes)

3. **Accessibility Requirements**:
   - Color-blind accessible design (icons + text, not color alone) (CF-R-042)
   - Dark mode for 3 AM waiting room (not blinding) (CF-R-024)

4. **Family Member Experience**:
   - Reassurance that patient is receiving care ("Currently Being Treated" section)
   - Prevent "kidnapped" anxiety when patient moves from waiting queue to treatment area
   - 15-minute visibility window for "In Treatment" status

---

### Technical Proficiency

**Level**: Basic

**Expertise**:
- Focus on patient experience and UX
- Represents patient voice in design decisions

---

### Pain Points

#### PP-2.1: Patient Identification Anxiety

**Quote**:
> "If they see a screen full of numbers, they feel like cattle. We need a humanized way to identify them that only they recognize." - Linda [Session 1.2, 11:08]

**Context**: Ticket-only identification systems dehumanize patients; patients forget numbers or lose paper slips

**Impact**: Patient anxiety increases; perception of being treated as "just a number"

**Severity**: P1

**Mitigation**: Privacy-compliant ID (JS-12) balances privacy with recognizability

---

#### PP-4.1: Countdown Timer Anxiety

**Quote**:
> "Do not show a countdown '59:59'. That causes riots." - Linda [Session 2.1 Cross-Check, 10:11]

**Context**: Real-time countdown timers increase patient anxiety and create perception of delays

**Impact**: Patients watch countdown obsessively; minute-by-minute tracking amplifies perceived wait time

**Severity**: P1

**Mitigation**: Category display (CF-R-034) instead of countdown timers ("Standard Wait" instead of "59:59")

---

### Key Quotes

#### Quote 1: Humanized Identification
> "Anxiety is a huge issue. If they see a screen full of numbers, they feel like cattle. We need a humanized way to identify them that only they recognize." - Linda [Session 1.2, 11:08]

**Analysis**: Pure numeric ticket systems fail UX requirements. Patients need semi-recognizable identifier.

---

#### Quote 2: Privacy ID Approval
> "'JS-12' is acceptable. It's obscure enough." - Linda [Session 1.2, 11:17]

**Analysis**: Confirms that Initials + Day format balances privacy with recognizability.

---

#### Quote 3: "Kidnapped" Anxiety
> "No! If I drop off the board, my husband thinks I've been kidnapped or I left. Keep me on the board but change status to 'In Treatment.'" - Linda [Session 1.2, 11:48]

**Analysis**: Family member anxiety when patient disappears from public display; requires two-section layout.

---

#### Quote 4: Two-Section Display Layout
> "A separate section at the bottom. 'Currently Being Treated: JS-12, AB-01...' Just a list. It reassures the family." - Linda [Session 1.2, 11:53]

**Analysis**: Defines two-section display layout requirement (CF-R-018).

---

#### Quote 5: No Countdown Timers
> "Correct. Do not show a countdown '59:59'. That causes riots. Show the category. 'Please wait approx 60 mins'." - Linda [Session 2.1 Cross-Check, 10:11]

**Analysis**: Rejects real-time countdown timers; category display preferred.

---

#### Quote 6: Dark Mode for Waiting Room
> "Actually, yes. A bright white TV in a dim waiting room at 3 AM is aggressive. Maybe the background is dark blue or charcoal, with white text?" - Linda [Session 2.1 Cross-Check, 10:33]

**Analysis**: Extends dark mode requirement to public display (not just nurse interfaces).

---

#### Quote 7: Color-Blind Accessibility
> "Yes. Or use shapes. Warning triangle vs Info circle." - Linda [Session 2.1 Cross-Check, 10:56]

**Analysis**: Advocates for redundant encoding (color + icons + text) for color-blind accessibility.

---

### Interface Requirements

**Public Display Design**:
- High readability (large fonts, ≥24px)
- High contrast (white text on dark background or dark text on light background)
- Two-section layout:
  - **Top Section**: Active waiting queue (JS-12 | Standard Wait | Waiting for Doctor)
  - **Bottom Section**: Currently being treated (JS-12, AB-01...)
- Category display, NOT countdown timers (CF-R-034)
- Dark mode (charcoal background, white text) for 3 AM visibility (CF-R-024)
- Color-blind accessible (icons + text, not color alone) (CF-R-042)
- Visual update notifications (blink/highlight when status changes) (CF-R-013)

---

### Traceability

**Client Facts**:
- CF-Q-005: Humanized identification
- CF-Q-007: Status message safety
- CF-Q-013: Category display, not countdown
- CF-Q-015: Dark mode for all interfaces
- CF-R-011: Privacy-compliant ID format (JS-12)
- CF-R-013: Real-time display update notification
- CF-R-018: Two-section display layout
- CF-R-021: "Rest" category label change (to "Standard Wait")
- CF-R-024: Dark mode for public display
- CF-R-034: Category display, not countdown timer
- CF-R-042: Color-blind accessible alerts

**Pain Points**:
- PP-2.1: Patient identification anxiety
- PP-4.1: Countdown timer anxiety

**User Type ID**: UT-2.3

---

## UT-3.1: IT Manager (Marcus - Client)

### Role Summary

**Primary Function**: Infrastructure approval (on-premise requirement), network segmentation, security policy enforcement

**Responsibility**: RBAC simplification decision, VM snapshot backups, security policy enforcement (SSL-only, LDAP)

**System Interaction**: Infrastructure monitoring dashboard (not part of pilot app)

**Traceability**: Identified in Session 1.3 (Infrastructure & Interoperability), Session 2.1 Security

---

### Detailed Responsibilities

1. **Infrastructure Approval**:
   - On-premise deployment requirement (NO cloud dependencies) (CF-C-004)
   - Network segmentation (VLAN 10: Server Farm, VLAN 40: Clinical & Kiosk)
   - Firewall rules (port 443 only, SSL-only even on LAN)

2. **Security Policy Enforcement**:
   - LDAP/Active Directory authentication (CF-R-027)
   - 15-minute idle timeout (CF-C-008)
   - Physical kiosk security (USB locks, restricted OS account)

3. **RBAC Simplification Decision**:
   - Choose trust-based model over granular RBAC (CF-R-043)
   - Two-role model: Clinical (full CRUD) vs View Only (kiosk)
   - Rationale: Human accountability over technical enforcement for pilot

4. **VM Snapshot Backups**:
   - Hourly VM snapshots (CF-R-048)
   - Crash-consistent recovery (PostgreSQL WAL)
   - Infrastructure team responsibility (not vendor)

5. **HL7 Interface Deferral**:
   - Reject EHR integration for pilot (CF-C-005)
   - Standalone system with double data entry
   - Trade-off: Speed prioritized over data integration

---

### Technical Proficiency

**Level**: Advanced

**Expertise**:
- Hospital IT infrastructure
- Network security and compliance
- Balances security vs usability trade-offs

---

### Pain Points

#### PP-3.1: Internet Dependency Risk

**Quote**:
> "Our internet cuts out during storms, but the internal LAN stays up. We cannot lose the waiting list if AWS goes down." - Marcus [Session 1.3, 13:10]

**Context**: Hospital internet outages during storms; cloud-based solutions unacceptable

**Impact**: System must remain operational during internet outages

**Severity**: P0

**Mitigation**: On-premise deployment (CF-C-004); Docker Compose on Kubernetes

---

#### PP-5.2: Session Timeout vs Data Loss

**Quote**:
> "Ideally, auto-save draft? But if that's too complex, then yes, data lost is better than unauthorized access." - Marcus [Session 2.1 Security, 14:49]

**Context**: 15-minute idle timeout may cause data loss if form half-filled

**Impact**: Security prioritized over convenience; data loss acceptable if auto-save too complex

**Severity**: P2

**Mitigation**: Security policy trumps user convenience; graceful error messaging

---

### Key Quotes

#### Quote 1: On-Premise Non-Negotiable
> "Web-based is fine, but no cloud. This needs to run On-Premise. Our internet cuts out during storms, but the internal LAN stays up. We cannot lose the waiting list if AWS goes down." - Marcus [Session 1.3, 13:10]

**Analysis**: Establishes hard constraint for on-premise deployment. Cloud-based solutions rejected outright.

---

#### Quote 2: No EHR Integration for Pilot
> "For this pilot? No. It's standalone. We don't have time to approve an HL7 interface. Double entry for now. Nurse types name in your app, and separately in Epic." - Marcus [Session 1.3, 13:21]

**Analysis**: HL7/FHIR integration deferred to future phases; pilot prioritizes speed.

---

#### Quote 3: Trust-Based RBAC Simplification
> "We trust our staff. Simplicity over granular restriction for this pilot. If someone messes up, we yell at them. We don't need code to prevent it." - Marcus [Session 2.1 Security, 14:31]

**Analysis**: Rejects complex role hierarchies in favor of two-role model (Clinical vs View-Only).

---

#### Quote 4: Physical Kiosk Security
> "The USB ports are physically blocked with locks. And the account has no shell access. It strictly launches Chrome in Kiosk mode pointing to `localhost`." - Marcus [Session 2.1 Security, 14:41]

**Analysis**: Multi-layer kiosk hardening: USB locks + restricted OS + Chrome kiosk mode.

---

#### Quote 5: Security Over Convenience (Idle Timeout)
> "Ideally, auto-save draft? But if that's too complex, then yes, data lost is better than unauthorized access." - Marcus [Session 2.1 Security, 14:49]

**Analysis**: Security policy trumps user convenience; 15-minute idle timeout enforced even if data lost.

---

#### Quote 6: VM Snapshot Backups
> "Snapshot the VM every hour. That's on us (Infrastructure). Your app just needs to be crash-consistent." - Marcus [Session 2.1 Security, 14:53]

**Analysis**: Infrastructure team handles backups; vendor ensures database crash consistency (WAL).

---

#### Quote 7: Air-Gapped Architecture
> "Correct. Air-gapped logic. Bundle everything. If it tries to phone home to `fonts.googleapis.com`, the firewall will drop it." - Marcus [Session 2.1 Security, 14:59]

**Analysis**: Security policy enforces air-gapped operation; no external dependencies.

---

### Interface Requirements

**Infrastructure Monitoring Dashboard** (not part of pilot app):
- Network firewall rules documentation
- LDAP authentication module status
- VM snapshot backup logs
- SSL certificate expiry monitoring

---

### Traceability

**Client Facts**:
- CF-Q-008: On-premise non-negotiable
- CF-Q-009: No EHR integration for pilot
- CF-Q-011: No external VPN access
- CF-Q-018: Trust-based RBAC simplification
- CF-Q-019: Physical kiosk security
- CF-Q-020: Security over convenience (idle timeout)
- CF-C-004: On-premise deployment constraint
- CF-C-005: No EHR integration (pilot constraint)
- CF-C-007: SSL-only on LAN (port 443)
- CF-C-008: 15-minute idle timeout
- CF-C-009: Air-gapped architecture (no CDNs)
- CF-C-010: Air-gapped bundle (reconfirmed)
- CF-R-027: LDAP/Active Directory authentication
- CF-R-043: Simplified RBAC (two roles)
- CF-R-046: Physical kiosk security
- CF-R-047: Session expiry handling
- CF-R-048: VM snapshot backups (hourly)

**Pain Points**:
- PP-3.1: Internet dependency risk
- PP-5.2: Session timeout vs data loss

**User Type ID**: UT-3.1

---

## UT-3.2: IT Ops Manager (Sheila - Client)

### Role Summary

**Primary Function**: VM provisioning, Docker Compose deployment, patching, SSL certificate distribution

**Responsibility**: Display hardware management (Chromebit, smart TV), VM snapshot backups (hourly)

**System Interaction**: Simple deployment script (one-liner), Docker Compose file

**Traceability**: Identified in Session 1.3 (Infrastructure & Interoperability)

---

### Detailed Responsibilities

1. **VM Provisioning**:
   - Ubuntu 22.04 LTS VM (4 vCPUs, 16GB RAM)
   - Kubernetes cluster for internal apps
   - Network segmentation (VLAN 10, VLAN 40)

2. **Docker Compose Deployment**:
   - Deploy containerized Node.js + PostgreSQL
   - Execute deployment script: `docker-compose down && docker-compose up -d`
   - Apply patches (Docker image tarball or git patch)

3. **SSL Certificate Distribution**:
   - Generate self-signed SSL certs for pilot
   - Push root CA to Chromebit and Nurse PCs via Group Policy

4. **Display Hardware Management**:
   - Configure Samsung TV (Tizen) + Chromebit
   - Chrome Kiosk mode setup (auto-launch → `https://localhost`)
   - Physical USB port locks (prevent keyboard attachment)

5. **VM Snapshot Backups**:
   - Hourly VM snapshots (CF-R-048)
   - Crash-consistent recovery validation

---

### Technical Proficiency

**Level**: Advanced

**Expertise**:
- DevOps (containerization, Kubernetes)
- Prefers automation and simplicity

---

### Pain Points

#### PP-6.1: Vendor VPN Access Blocked

**Quote**:
> "No external VPN access for vendors without a 2-week approval process." - Sheila [Session 1.3, 13:43]

**Context**: Security policy creates friction for rapid patching; vendor cannot VPN in

**Impact**: Critical bug fixes require manual tarball delivery and IT Ops application; no direct remote access

**Severity**: P1

**Mitigation**: Simple deployment script (CF-R-030); vendor sends Docker image tarball or git patch

---

### Key Quotes

#### Quote 1: Kubernetes Cluster Available
> "Yes, we have a Kubernetes cluster for internal apps. But you need to handle the display hardware." - Sheila [Session 1.3, 13:13]

**Analysis**: Confirms infrastructure availability; vendor responsible for display hardware setup.

---

#### Quote 2: Sub-Second Display Latency
> "Sub-second. If a patient sees the doctor click and the screen doesn't change, they start knocking on the glass." - Sheila [Session 1.3, 13:26]

**Analysis**: Reinforces real-time requirement; WebSocket architecture mandatory.

---

#### Quote 3: Postgres Containerization
> "We prefer Postgres for reliability, but if you containerize it, I don't care." - Sheila [Session 1.3, 13:33]

**Analysis**: Containerized Postgres acceptable; no bare-metal database installation.

---

#### Quote 4: No Vendor VPN Access
> "No external VPN access for vendors without a 2-week approval process. You will send me a new Docker image tarball, or a git patch. I will apply it." - Sheila [Session 1.3, 13:43]

**Analysis**: Security policy blocks vendor VPN access; patching workflow must be dead simple.

---

#### Quote 5: Simple Deployment Script
> "Keep the deployment script dead simple. `docker-compose down && docker-compose up -d`." - Sheila [Session 1.3, 13:43]

**Analysis**: One-liner deployment command reduces risk of IT Ops errors.

---

#### Quote 6: VM Snapshot Backups
> "Snapshot the VM every hour. That's on us (Infrastructure). Your app just needs to be crash-consistent." - Sheila [Session 1.3, 13:59]

**Analysis**: Infrastructure team handles backups; vendor ensures database crash consistency.

---

### Interface Requirements

**Deployment Documentation**:
- Docker Compose file with clear instructions
- One-liner deployment script: `docker-compose down && docker-compose up -d`
- SSL certificate generation guide (self-signed certs)
- Chromebit setup guide (Chrome Kiosk mode)
- Network firewall rules (port 443 only)

---

### Traceability

**Client Facts**:
- CF-Q-010: Sub-second display latency
- CF-Q-011: No external VPN access
- CF-C-006: No vendor VPN access
- CF-R-022: Sub-second display latency (WebSocket)
- CF-R-025: Docker Compose deployment
- CF-R-026: Postgres in container (not SQLite)
- CF-R-030: Simple deployment script
- CF-R-033: NTP time synchronization
- CF-R-048: VM snapshot backups (hourly)

**Pain Points**:
- PP-6.1: Vendor VPN access blocked

**User Type ID**: UT-3.2

---

## UT-3.3: Interoperability Specialist (Raj - Vendor)

### Role Summary

**Primary Function**: HL7/FHIR integration assessment, data mismatch risk analysis

**Responsibility**: Evaluate EHR integration feasibility, identify double-entry risks

**System Interaction**: Not applicable (no EHR integration for pilot)

**Traceability**: Identified in Session 1.3 (Infrastructure & Interoperability)

---

### Detailed Responsibilities

1. **HL7/FHIR Integration Assessment**:
   - Evaluate feasibility of Epic/Cerner integration
   - Recommend HL7 interface vs standalone approach
   - Assess approval timelines (2-3 months for HL7 interface)

2. **Data Mismatch Risk Analysis**:
   - Identify double-entry typo risks (e.g., "Jonh Smith" vs "John Smith")
   - Recommend data validation strategies
   - Accept pilot trade-off: Double-entry acceptable for pilot phase

---

### Technical Proficiency

**Level**: Advanced

**Expertise**:
- Healthcare interoperability standards (HL7, FHIR)
- EHR integration (Epic, Cerner)

---

### Pain Points

#### PP-3.2: Data Integrity (Double Entry Risk)

**Quote**:
> "What if Jenny types 'Jonh Smith' in your app and 'John Smith' in Epic?" - Raj [Session 1.3, 13:35]

**Context**: Typos in standalone system won't match EHR records

**Impact**: Data mismatch between Ragus and Epic; patient record discrepancies

**Severity**: P2

**Mitigation**: Accepted risk for pilot; HL7 integration deferred to future phases

---

### Key Quotes

#### Quote 1: EHR Integration Assessment
> "Do we need to pull patient demographics from your main EHR (Epic/Cerner)?" - Raj [Session 1.3, 13:15]

**Analysis**: Evaluates need for HL7/FHIR integration; deferred for pilot.

---

#### Quote 2: Double-Entry Data Mismatch Risk
> "Back to the 'Double Entry.' I'm worried about data mismatch. What if Jenny types 'Jonh Smith' in your app and 'John Smith' in Epic?" - Raj [Session 1.3, 13:35]

**Analysis**: Identifies data integrity risk; accepted as pilot-appropriate trade-off.

---

### Interface Requirements

Not applicable (no EHR integration for pilot)

---

### Traceability

**Client Facts**:
- CF-Q-009: No EHR integration for pilot
- CF-C-005: No EHR integration (pilot constraint)

**Pain Points**:
- PP-3.2: Data integrity (double entry risk)

**User Type ID**: UT-3.3

---

## UT-4.1: Float Nurse (Temporary Staff)

### Role Summary

**Primary Function**: Fill in for Jenny (Intake Nurse) during vacations

**Responsibility**: Perform basic intake tasks (Name, DOB, Complaint) with zero training

**System Interaction**: Intake screen (same as Jenny, UT-1.1)

**Traceability**: Identified in Session 2.1 Cross-Check

---

### Detailed Responsibilities

1. **Basic Intake Tasks**:
   - Capture Name, DOB, Gender, Complaint, Allergies
   - Generate privacy ID (JS-12)
   - Add patient to pre-triage queue

2. **Zero-Training Constraint**:
   - Learn system in 30 seconds
   - No training manual available
   - Self-explanatory UI required

---

### Technical Proficiency

**Level**: Basic

**Constraint**: Zero training available; must learn system in 30 seconds

---

### Pain Points

#### PP-4.3: Zero-Training Constraint

**Quote** (from Carol):
> "If Jenny takes a vacation and we have a float nurse, she needs to figure it out in 30 seconds. Big labels. 'ADD PATIENT.' 'SAVE.' No hidden menus." - Carol [Session 2.1 Cross-Check, 10:49]

**Context**: Float nurses fill in during vacations; no training time available

**Impact**: Complex UI blocks temporary staff; causes workflow disruptions

**Severity**: P1

**Mitigation**: Self-explanatory UI with big labels (CF-R-040); no hidden menus

---

### Key Quotes

(All quotes from Carol describing float nurse requirements)

> "Zero. It needs to be intuitive. If Jenny takes a vacation and we have a float nurse, she needs to figure it out in 30 seconds. Big labels. 'ADD PATIENT.' 'SAVE.' No hidden menus." - Carol [Session 2.1 Cross-Check, 10:49]

**Analysis**: Defines hard constraint for self-explanatory UI; no training budget.

---

### Interface Requirements

**Same as UT-1.1 (Intake Nurse) with emphasis on**:
- Big labels: "ADD PATIENT", "SAVE", "NEXT"
- No hidden menus or complex workflows
- Self-explanatory UI (30-second onboarding)
- Visual affordances (buttons look clickable)

---

### Traceability

**Client Facts**:
- CF-Q-016: Zero-training mandate (Carol's quote)
- CF-R-040: Zero-training UX design

**Pain Points**:
- PP-4.3: Zero-training constraint

**User Type ID**: UT-4.1

---

## UT-5.1: Security Specialist (Sam - Vendor)

### Role Summary

**Primary Function**: RBAC design and simplification, audit logging requirements, physical kiosk security validation

**Responsibility**: Session management policies, security architecture expertise

**System Interaction**: Audit logging dashboard (for security review, not daily use)

**Traceability**: Identified in Session 2.1 Security

---

### Detailed Responsibilities

1. **RBAC Design and Simplification**:
   - Propose granular RBAC (Intake Nurse, Triage Nurse, Doctor roles)
   - Accept client decision for trust-based model (CF-R-043)

2. **Audit Logging Requirements**:
   - Define action logging format (CF-R-045)
   - Pseudonymized patient IDs only (no PHI beyond pseudonym)
   - 30-day retention for audit trail

3. **Physical Kiosk Security Validation**:
   - Validate multi-layer kiosk hardening (USB locks, restricted OS, Chrome Kiosk mode)
   - Assess re-identification risks

4. **Session Management Policies**:
   - Define 15-minute idle timeout (CF-C-008)
   - Graceful session expiry handling (CF-R-047)

---

### Technical Proficiency

**Level**: Advanced

**Expertise**:
- Security architecture
- GDPR compliance
- Risk assessment

---

### Pain Points

None extracted (consultant/advocate role)

---

### Key Quotes

#### Quote 1: RBAC Proposal
> "Let's talk about Role-Based Access Control (RBAC). Intake Nurse: Can Create, Edit. Triage Nurse: Can Edit (Vitals, ESI). Doctor: Can Edit (Time Slots, Discharge). Admin: Can Config?" - Sam [Session 2.1 Security, 14:22]

**Analysis**: Proposes granular RBAC; client chooses trust-based model instead.

---

#### Quote 2: Trust-Based Model Concern
> "That simplifies things, but it means a junior nurse *could* mess with the board." - Sam [Session 2.1 Security, 14:27]

**Analysis**: Identifies risk of trust-based model; client accepts risk for pilot.

---

#### Quote 3: Audit Logging
> "Audit Logging. Even if we don't keep patient data, we should log *actions*. 'User X moved Patient Y to 30m'." - Sam [Session 2.1 Security, 14:35]

**Analysis**: Defines audit trail requirement with pseudonymized patient IDs.

---

#### Quote 4: Physical Security
> "Physical security. The server. Is it in a locked rack?" - Sam [Session 2.1 Security, 14:40]

**Analysis**: Validates server physical security (locked rack, access control).

---

#### Quote 5: Session Management
> "Session management. If Dr. Evans leaves his Surface on the desk, does it auto-logout?" - Sam [Session 2.1 Security, 14:45]

**Analysis**: Identifies idle timeout requirement (15 minutes).

---

#### Quote 6: Backups
> "Backups. We agreed on ephemeral data, but if the database corrupts at 2 PM, we need to restore the morning's intake." - Sam [Session 2.1 Security, 14:52]

**Analysis**: Validates VM snapshot backup strategy (hourly).

---

#### Quote 7: Air-Gapped Architecture
> "Final check. No external APIs? No Google Fonts, no CDNs?" - Sam [Session 2.1 Security, 14:58]

**Analysis**: Confirms air-gapped architecture requirement.

---

### Interface Requirements

**Audit Logging Dashboard** (for security review, not daily use):
- Action logs with pseudonymized patient IDs
- 30-day retention compliance
- Session expiry events
- Failed login attempts

---

### Traceability

**Client Facts**:
- CF-C-008: 15-minute idle timeout
- CF-C-010: Air-gapped bundle
- CF-R-027: LDAP authentication
- CF-R-043: Simplified RBAC (two roles)
- CF-R-045: Audit logging (action trail)
- CF-R-046: Physical kiosk security
- CF-R-047: Session expiry handling
- CF-R-048: VM snapshot backups (hourly)
- CF-R-049: Database crash consistency (WAL)

**Pain Points**: None (consultant/advocate role)

**User Type ID**: UT-5.1

---

## User Type Summary Table

| User Type | Name | Role | Technical Proficiency | Primary Pain Points | Key Requirements |
|-----------|------|------|----------------------|---------------------|------------------|
| **UT-1.1** | Jenny | Intake Nurse | Basic | PP-1.1: Slow intake workflow | Minimal fields, touchscreen, big buttons |
| **UT-1.2** | Carol | Triage Nurse (Head Nurse) | Basic | PP-1.2: Triage bottleneck<br>PP-1.3: Gloved hands UX<br>PP-4.3: Zero-training<br>PP-4.4: Night shift eye strain | Big buttons, dark mode, zero-training UX |
| **UT-1.3** | Dr. Evans | Triage Doctor | Basic | PP-4.2: Auto-escalation safety risk<br>PP-5.2: Aggressive patient safety | Kanban board, progressive alerts, one-click actions |
| **UT-2.1** | Elena | Data Privacy Officer (Vendor) | Advanced | None (enforcer role) | Privacy audit dashboard, compliance validation |
| **UT-2.2** | Dr. Halloway | GDPR Lead (Client) | Intermediate | PP-2.2: Privacy vs usability conflict<br>PP-5.1: Data liability risk | Privacy audit report, ephemeral data storage |
| **UT-2.3** | Linda | Patient Rights Rep (Client) | Basic | PP-2.1: Patient ID anxiety<br>PP-4.1: Countdown timer anxiety | Two-section display, category display, dark mode |
| **UT-3.1** | Marcus | IT Manager (Client) | Advanced | PP-3.1: Internet dependency risk<br>PP-5.2: Session timeout vs data loss | On-premise deployment, SSL-only, LDAP auth |
| **UT-3.2** | Sheila | IT Ops Manager (Client) | Advanced | PP-6.1: Vendor VPN access blocked | Simple deployment script, Docker Compose |
| **UT-3.3** | Raj | Interoperability Specialist (Vendor) | Advanced | PP-3.2: Data integrity (double entry) | HL7/FHIR assessment (deferred for pilot) |
| **UT-4.1** | Float Nurse | Temporary Staff | Basic | PP-4.3: Zero-training constraint | Self-explanatory UI, big labels, no hidden menus |
| **UT-5.1** | Sam | Security Specialist (Vendor) | Advanced | None (consultant role) | Audit logging, session management, physical security |

---

## Role Interactions & Dependencies

### Clinical Staff Workflow (UT-1.1 → UT-1.2 → UT-1.3)

```
Intake Nurse (Jenny, UT-1.1)
   ↓ Creates patient record (State 1: Intake Complete)
Triage Nurse (Carol, UT-1.2)
   ↓ Captures vitals + ESI (State 2: Triage In-Progress)
Triage Doctor (Dr. Evans, UT-1.3)
   ↓ Assigns time slot (State 4: Time Slot Assigned)
[Patient called to treatment]
```

**Dependencies**:
- UT-1.2 depends on UT-1.1 completing minimal intake fields
- UT-1.3 depends on UT-1.2 completing triage (vitals + ESI)
- Float Nurse (UT-4.1) can substitute for UT-1.1 during vacations

---

### Privacy & Compliance Triad (UT-2.1, UT-2.2, UT-2.3)

```
Data Privacy Officer (Elena, UT-2.1) → Enforces GDPR/HIPAA compliance
GDPR Lead (Dr. Halloway, UT-2.2) → Veto authority on privacy decisions
Patient Rights Rep (Linda, UT-2.3) → Advocates for patient dignity
```

**Collaboration**:
- UT-2.1 proposes privacy-compliant ID format → UT-2.2 validates re-identification risk → UT-2.3 confirms patient acceptability
- All three roles approve safe status message enum (CF-R-017)
- All three roles approve two-section display layout (CF-R-018)

---

### Infrastructure Triad (UT-3.1, UT-3.2, UT-3.3)

```
IT Manager (Marcus, UT-3.1) → Approves on-premise deployment, RBAC simplification
IT Ops Manager (Sheila, UT-3.2) → Deploys Docker Compose, applies patches
Interoperability Specialist (Raj, UT-3.3) → Assesses EHR integration feasibility
```

**Dependencies**:
- UT-3.2 deploys infrastructure defined by UT-3.1
- UT-3.3 identifies data mismatch risks → UT-3.1 accepts double-entry trade-off for pilot

---

### Security Specialists (UT-5.1) → Consults with IT Manager (UT-3.1)

```
Security Specialist (Sam, UT-5.1) → Proposes RBAC, audit logging, session management
IT Manager (Marcus, UT-3.1) → Makes final decisions (trust-based RBAC, 15-min timeout)
```

**Collaboration**:
- UT-5.1 proposes granular RBAC → UT-3.1 chooses trust-based model
- UT-5.1 defines audit logging requirements → UT-3.1 approves 30-day retention

---

## Cross-Role Requirements Summary

### Zero-Training UX (Affects UT-1.1, UT-1.2, UT-4.1)

**Requirement**: UI must be self-explanatory in 30 seconds (CF-R-040)

**Design Principles**:
- Big labels: "ADD PATIENT", "SAVE", "NEXT"
- No hidden menus or complex interactions
- Self-explanatory workflows
- Visual affordances (buttons look clickable)

**Affected Roles**:
- UT-1.1 (Jenny, Intake Nurse): Primary user of intake screen
- UT-1.2 (Carol, Head Nurse): Primary user of triage screen; trains float nurses
- UT-4.1 (Float Nurse): Temporary staff with zero training

---

### Dark Mode (Affects UT-1.1, UT-1.2, UT-1.3, UT-2.3)

**Requirement**: Dark mode support for all interfaces (CF-R-023, CF-R-024)

**Scope**:
- Intake/Triage View (UT-1.1, UT-1.2, UT-4.1)
- Doctor Dashboard (UT-1.3)
- Public Display (UT-2.3 advocacy)

**Design**:
- High contrast (white text on dark background)
- Charcoal or dark blue background (not pure black)
- Avoid bright white in 3 AM waiting room

---

### Privacy Compliance (Affects UT-2.1, UT-2.2, UT-2.3, UT-1.1, UT-1.2, UT-1.3)

**Requirement**: NO PII on public displays (CF-C-001, CF-R-011)

**Format**: Privacy-compliant ID (JS-12 = Initials + Day)

**Scope**:
- Clinical staff (UT-1.1, UT-1.2, UT-1.3) see full patient data internally
- Public display (UT-2.3 validation) shows ONLY pseudonym ID (JS-12)
- Compliance officers (UT-2.1, UT-2.2) enforce and validate

---

### On-Premise Deployment (Affects UT-3.1, UT-3.2, UT-1.1, UT-1.2, UT-1.3)

**Requirement**: No cloud dependencies (CF-C-004)

**Context**: Hospital internet cuts out during storms; internal LAN remains operational

**Scope**:
- Infrastructure (UT-3.1, UT-3.2) deploys Docker Compose on Kubernetes
- Clinical staff (UT-1.1, UT-1.2, UT-1.3) continue using system during internet outages

---

## Version History

| Version | Date | Author | Changes | Feedback Ref |
|---------|------|--------|---------|--------------|
| 1.0.0 | 2026-02-16 | Discovery_InterviewAnalyst | Initial role synthesis across 5 sessions | FB-001 |
