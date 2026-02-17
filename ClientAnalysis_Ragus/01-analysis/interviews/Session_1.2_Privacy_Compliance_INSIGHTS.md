---
artifact_type: interview_analysis
interview_id: IVA-002
session_id: Session_1.2
system_name: Ragus
stage: Discovery
created_at: 2026-02-16
version: 1.0.0
author: Discovery_InterviewAnalyst
status: completed
feedback_ref: FB-001
---

# Interview Analysis: Session 1.2 - Privacy & Compliance Barrier

## Interview Metadata

| Field | Value |
|-------|-------|
| **Session ID** | Session_1.2 |
| **Focus** | The Public Display Board logic and Privacy Constraints |
| **Duration** | 11:00 AM – 12:00 PM |
| **Date** | [Interview Date from Source] |
| **Participants (Vendor)** | Elena (Data Privacy Officer), Sam (IT Security) |
| **Participants (Client)** | Dr. Halloway (GDPR Lead), Linda (Patient Rights Rep) |

## Executive Summary

This session focused exclusively on GDPR/HIPAA compliance requirements for the public waiting room display board. Key findings establish the critical constraint that no personally identifiable information (full names, medical conditions) can be displayed, leading to the design of a privacy-compliant pseudonym system using initials plus birth day ("JS-12" format). The session also defined safe status message enums and data retention policies.

**Primary Findings**:
- 15 client facts extracted
- 2 pain points identified (PP-2.1, PP-2.2)
- 3 user types profiled (Data Privacy Officer, GDPR Lead, Patient Rights Rep)
- Privacy-compliant ID format established (Initials + Day + Suffix)
- Safe status message enum defined (4 states)

---

## Pain Points Extracted

### PP-2.1: Patient Identification Anxiety
- **Quote**: "If they see a screen full of numbers, they feel like cattle. We need a humanized way to identify them that only they recognize." - Linda [11:08]
- **Severity**: P1
- **Category**: Patient Experience
- **Impact**: Ticket-only identification causes anxiety and dehumanization; patients forget numbers or lose paper slips
- **User Type**: UT-2.3 (Patient Rights Rep - Linda)
- **Trace**: CF-Q-004, CF-R-011

### PP-2.2: Privacy vs Usability Conflict
- **Quote**: "Too risky. In a small town, everyone knows 'John S.' with a broken arm is John Smith the baker." - Dr. Halloway [11:11]
- **Severity**: P0
- **Category**: Privacy Compliance
- **Impact**: Traditional display methods (full names or "First + Initial") violate GDPR/HIPAA in small communities where everyone knows each other
- **User Type**: UT-2.2 (GDPR Lead - Dr. Halloway)
- **Trace**: CF-C-001, CF-R-011

---

## Key Quotes

### CF-Q-004: Privacy Non-Negotiable
> "Under GDPR and HIPAA, we cannot display names. 'John Smith: 30 minutes' is a violation. This is non-negotiable." - Elena [11:05], Dr. Halloway [11:06]

**Analysis**: Establishes the absolute requirement for privacy-compliant patient identification. No exceptions, no full names, no medical conditions on public display.

### CF-Q-005: Humanized Identification
> "If they see a screen full of numbers, they feel like cattle. We need a humanized way to identify them that only they recognize." - Linda [11:08]

**Analysis**: Pure numeric ticket systems fail UX requirements. Patients need a semi-recognizable identifier that balances privacy with human dignity.

### CF-Q-006: Small Town Re-Identification Risk
> "Too risky. In a small town, everyone knows 'John S.' with a broken arm is John Smith the baker." - Dr. Halloway [11:11]

**Analysis**: First Name + Initial format rejected due to small community re-identification risk. Context (injury type, timing) can reveal identity even with partial names.

### CF-Q-007: Status Message Safety
> "Do NOT show 'Transfer to Psych.'" - Linda [11:36]

**Analysis**: Status messages must be clinically neutral. Psychiatric or sensitive dispositions cannot be displayed to protect patient dignity and HIPAA compliance.

---

## Workflow Observations

### Privacy-Compliant ID Generation

```
Input: Patient Name (John Smith), DOB (12th of any month)
Output: JS-12

Collision Handling:
1. Check if "JS-12" exists in active queue
2. If collision detected:
   - Option A: Append month (JS-12-Jan vs JS-12-Dec)
   - Option B: Append sequence suffix (JS-12-A, JS-12-B)
3. Preferred: Simple suffix (keeps ID short for readability)

Special Cases:
- Unidentified/Trauma patients: Use temporary alias from EHR ("Trauma Alpha")
- Manual override: Intake Nurse can manually set ID if needed (CF-R-016)
```

### Safe Status Message Enum

**Approved Status Messages** (Fixed, Non-Sensitive):
1. "Waiting for Triage"
2. "Waiting for Doctor"
3. "With Doctor" / "In Treatment"
4. "Results Pending"

**Prohibited Status Messages**:
- Any psychiatric references ("Transfer to Psych")
- Specific medical procedures
- Disposition details beyond generic "In Treatment"

### Display Sections (Two-Part Layout)

**Primary Section (Top)**: Active waiting queue
- Shows patients with assigned wait times (30m, 60m, 120m, Rest)
- Format: `JS-12 | Standard Wait | Status`

**Secondary Section (Bottom)**: Currently being treated
- Format: `Currently Being Treated: JS-12, AB-01...`
- Duration: Show for 15 minutes after entering treatment, then remove
- Purpose: Reassures family members that patient is receiving care

---

## Requirements Extracted

### CF-C-001: GDPR/HIPAA Privacy Compliance (HARD CONSTRAINT)
- **Source**: Elena [11:05], Dr. Halloway [11:06]
- **Constraint**: NO full names, NO medical conditions on public display
- **Rationale**: Legal requirement, non-negotiable
- **Enforcement**: Privacy audit required before deployment

### CF-R-011: Privacy-Compliant Patient ID Format
- **Source**: Elena [11:15], Dr. Halloway [11:17], Linda [11:17]
- **Requirement**: Patient ID format = Initials + Day of Birth + Suffix (if collision)
  - Example: "John Smith" born 12th = "JS-12"
  - Collision: "JS-12-A", "JS-12-B" (simple suffix preferred over month)
- **Display**: `Your ID | Estimated Wait | Status`
- **Rationale**: Balances privacy with recognizability; obscure enough to prevent re-identification

### CF-R-012: No Medical Complaint Display
- **Source**: Sam [11:20], Dr. Halloway [11:21]
- **Requirement**: Public display shows ONLY Time Category, NOT chief complaint
- **Prohibition**: NEVER show `JS-12 | Hemorrhoids | 30 mins`
- **Rationale**: Medical privacy, patient dignity

### CF-R-013: Real-time Display Update Notification
- **Source**: Elena [11:22], Linda [11:23]
- **Requirement**: When doctor changes time estimate (60m → 30m), public display updates
- **No Mobile App**: For pilot, no SMS/push notifications
- **Visual Alert**: Screen should blink or highlight when status changes
- **Rationale**: Manages patient expectations, reduces inquiry load at reception

### CF-R-014: Collision Detection Logic
- **Source**: Elena [11:25], Dr. Halloway [11:26], Linda [11:28]
- **Requirement**: System detects duplicate IDs in active queue
- **Action**: If "JS-12" already exists, prompt Intake Nurse
- **Suffix Options**:
  - Month: "JS-12-Jan" vs "JS-12-Dec"
  - Sequence: "JS-12-A", "JS-12-B" (PREFERRED - shorter, more readable)
- **Constraint**: Keep ID short for cross-room readability

### CF-R-015: Unidentified Patient Handling
- **Source**: Sam [11:30], Dr. Halloway [11:32]
- **Requirement**: For "Jane Doe" or unidentified stable patients, use temporary alias from EHR
- **Example**: "Trauma Alpha" (if patient bypasses intake but is stable)
- **Note**: Critical trauma cases bypass waiting room entirely (not on board)
- **Manual Override**: Intake Nurse can manually override ID field if necessary

### CF-R-016: Manual ID Override Capability
- **Source**: Dr. Halloway [11:32]
- **Requirement**: Intake Nurse can manually set the "ID" field for edge cases
- **Use Case**: Unidentified patients, system-generated ID is unclear
- **Rationale**: Clinical flexibility for non-standard scenarios

### CF-R-017: Safe Status Message Enum
- **Source**: Elena [11:39-11:43], Dr. Halloway [11:41], Linda [11:42]
- **Requirement**: Status messages must be fixed, clinically neutral enum
- **Approved Messages**:
  1. "Waiting for Triage"
  2. "Waiting for Doctor"
  3. "With Doctor" / "In Treatment"
  4. "Results Pending"
- **Prohibited**: Any psychiatric, sensitive disposition messages (e.g., "Transfer to Psych")
- **Rationale**: HIPAA compliance, patient dignity

### CF-R-018: Two-Section Display Layout
- **Source**: Dr. Halloway [11:43-11:46], Linda [11:48], Linda [11:53]
- **Requirement**:
  - **Top Section**: Active waiting queue (patients with assigned wait times)
  - **Bottom Section**: "Currently Being Treated" list (JS-12, AB-01...)
- **Duration**: Keep in "In Treatment" section for 15 minutes, then remove
- **Rationale**: Reassures family members, prevents "kidnapped" anxiety

### CF-R-019: Data Retention Policy (30 Days)
- **Source**: Elena [11:50], Dr. Halloway [11:52]
- **Requirement**: Server logs kept for 30 days, then rotated
- **Scope**: For pilot, testing *flow*, not legal defense
- **Constraint**: NO historical data displayed on frontend (backend audit trail only)
- **Rationale**: GDPR data minimization, pilot-appropriate retention

### CF-R-021: "Rest" Category Label Change
- **Source**: Sam [11:55], Linda [11:57]
- **Requirement**: Replace "Rest" label with "Standard Wait" or "Awaiting Assessment"
- **Final Choice**: "Standard Wait"
- **Rationale**: "Rest" sounds like telling patients to nap; "Standard Wait" lowers expectations appropriately

---

## Role Profiles

### UT-2.1: Data Privacy Officer (Elena - Vendor)

**Responsibilities**:
- GDPR/HIPAA compliance enforcement
- Privacy-compliant ID design
- Data retention policy definition
- Audit trail requirements

**Technical Proficiency**: Advanced
- Understands regulatory frameworks
- Designs privacy-by-design systems

**Pain Points**: None extracted (advocate/enforcer role)

**Quotes**:
- "Under GDPR and HIPAA, we cannot display names. 'John Smith: 30 minutes' is a violation."
- "Proposal: When Jenny does the intake, the system assigns a pseudonym or a 'Call Name' that is printed on a wristband?"
- "Data minimization. How long do we keep the logs?"

**Interface Requirements**:
- Compliance audit dashboard (for validation, not daily use)
- Audit logs with pseudonymized IDs (hashed or JS-12 format)

---

### UT-2.2: GDPR Lead (Dr. Halloway - Client)

**Responsibilities**:
- GDPR compliance veto authority
- Privacy risk assessment (small town re-identification)
- Data retention policy approval
- Status message safety validation

**Technical Proficiency**: Intermediate
- Legal/compliance background
- Understands GDPR/HIPAA implications

**Pain Points**:
- PP-2.2: Privacy vs usability conflict (rejects "First + Initial" format)

**Quotes**:
- "Correct. This is non-negotiable."
- "Too risky. In a small town, everyone knows 'John S.' with a broken arm is John Smith the baker."
- "It's rare, but statistically possible. The system needs to detect that [collision]."
- "Do NOT show 'Transfer to Psych.'"

**Interface Requirements**:
- Privacy audit report (pre-deployment validation)
- Compliance dashboard showing sensitive data exposure risks

---

### UT-2.3: Patient Rights Rep (Linda)

**Responsibilities**:
- Patient advocacy (dignity, anxiety reduction)
- Display clarity validation
- Accessibility requirements (color-blind, readability)
- Family member experience (reassurance)

**Technical Proficiency**: Basic
- Focus on UX and patient experience
- Represents patient voice in design decisions

**Pain Points**:
- PP-2.1: Patient identification anxiety (ticket-only systems dehumanize)

**Quotes**:
- "Anxiety is a huge issue. If they see a screen full of numbers, they feel like cattle."
- "'JS-12' is acceptable. It's obscure enough."
- "No! If I drop off the board, my husband thinks I've been kidnapped or I left. Keep me on the board but change status to 'In Treatment.'"
- "A separate section at the bottom. 'Currently Being Treated: JS-12, AB-01...' Just a list. It reassures the family."

**Interface Requirements**:
- High readability (large fonts, high contrast)
- Two-section layout (waiting queue + in-treatment list)
- Visual update notifications (blink/highlight)

---

## Observations

### Privacy Design Constraints

1. **Small Community Context**: Traditional partial identifiers (First + Initial) fail in small towns where social context enables re-identification.
2. **Pseudonym Requirements**: ID must be obscure enough to prevent casual re-identification but recognizable enough for patients to self-identify.
3. **No Medical Context**: Time categories only; no chief complaints, procedures, or dispositions on public display.

### Collision Handling Strategy

1. **Rarity vs Complexity**: Collisions are statistically rare but must be handled gracefully.
2. **Simplicity Wins**: Simple suffix ("JS-12-A", "JS-12-B") preferred over complex month-based identifiers for readability.
3. **Manual Override**: Nurse discretion allows for edge cases (unidentified patients, system errors).

### Family Member Experience

1. **"Kidnapped" Anxiety**: Linda's concern about disappearing from the board reflects family member anxiety when patients move to treatment areas.
2. **15-Minute Visibility Window**: Showing "In Treatment" status for 15 minutes balances reassurance with board clutter.
3. **Status Updates**: Visual alerts (blink/highlight) when wait time changes reduce reception inquiry load.

### Data Retention Balance

1. **Audit Trail vs Data Minimization**: 30-day retention for complaint resolution vs GDPR data minimization principle.
2. **Pilot-Appropriate**: For pilot, prioritizing flow testing over legal defensibility.
3. **No Frontend History**: Logs stored backend only; no historical data exposed to UI.

---

## Traceability Links

### Client Facts
- CF-Q-004: Privacy non-negotiable (Elena, Dr. Halloway)
- CF-Q-005: Humanized identification (Linda)
- CF-Q-006: Small town re-identification risk (Dr. Halloway)
- CF-Q-007: Status message safety (Linda)
- CF-C-001: GDPR/HIPAA compliance constraint
- CF-R-011: Privacy-compliant ID format (JS-12)
- CF-R-012: No medical complaint display
- CF-R-013: Real-time display update notification
- CF-R-014: Collision detection logic
- CF-R-015: Unidentified patient handling
- CF-R-016: Manual ID override capability
- CF-R-017: Safe status message enum
- CF-R-018: Two-section display layout
- CF-R-019: Data retention policy (30 days)
- CF-R-021: "Rest" category label change

### Pain Points
- PP-2.1: Patient identification anxiety
- PP-2.2: Privacy vs usability conflict

### User Types
- UT-2.1: Data Privacy Officer (Elena)
- UT-2.2: GDPR Lead (Dr. Halloway)
- UT-2.3: Patient Rights Rep (Linda)

---

## Next Steps

1. **Privacy Audit**: Pre-deployment compliance validation checklist
2. **Collision Detection**: Implement real-time duplicate ID detection at intake
3. **Display Layout**: Wireframes for two-section display (waiting queue + in-treatment)
4. **Status Message Enum**: Hardcode safe status messages in frontend/backend
5. **Data Retention**: Implement 30-day rotation cron job

---

## Version History

| Version | Date | Author | Changes | Feedback Ref |
|---------|------|--------|---------|--------------|
| 1.0.0 | 2026-02-16 | Discovery_InterviewAnalyst | Initial interview analysis | FB-001 |
