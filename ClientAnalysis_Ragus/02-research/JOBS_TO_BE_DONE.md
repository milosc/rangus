---
document_id: DISC-JTBD-Ragus
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GenerateJTBD
source_files:
  - 02-research/persona-intake-nurse.md
  - 02-research/persona-triage-nurse.md
  - 02-research/persona-triage-doctor.md
  - 02-research/persona-patient-advocate.md
  - 02-research/persona-it-compliance-lead.md
  - traceability/pain_points_registry.json
---

# Jobs-To-Be-Done: Ragus

**Version**: 1.0.0
**Created**: 2026-02-16

---

## Executive Summary

This document captures the Jobs-To-Be-Done (JTBD) for the Ragus emergency room triage system, derived from persona analysis and pain point research conducted through client interviews. Jobs are organized by persona and prioritized based on frequency, importance, and connection to identified pain points.

**Total Jobs Identified**: 28
- Functional Jobs: 23
- Emotional Jobs: 4
- Social Jobs: 1

**Key Insight**: Clinical staff need ultra-fast data entry with glove-friendly touchscreen interfaces, while patients need humane identification methods that preserve privacy. The system must work offline during internet outages and provide real-time updates without causing patient anxiety.

---

## JTBD Framework

Each job follows the structure:
```
When [situation], I want to [motivation], so I can [expected outcome].
```

Jobs are rated on:
- **Frequency**: How often the job occurs (Daily, Weekly, Monthly, Quarterly)
- **Importance**: Critical, High, Medium, Low
- **Satisfaction**: Current satisfaction with existing solution (1-5)

---

## P-1.1: Intake Nurse (Jenny) Jobs

### JTBD-1.1: Process Urgent Patients Instantly

**Statement**: When a trauma or critical patient arrives at the ER, I want to complete intake registration in under 30 seconds, so I can prevent dangerous delays during life-threatening situations.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (5-10 times/day, more during high-volume periods) |
| Importance | Critical |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-1.1 |
| Related Gaps | GAP-001 (Fast intake form) |

**Job Steps**:
1. Patient arrives (trauma, cardiac event, severe injury)
2. Capture essential information: Name, DOB, Chief Complaint
3. Skip optional fields to minimize typing
4. Submit intake and send patient to triage
5. Complete remaining details after patient is with clinical staff

**Success Criteria**:
- Intake time <30 seconds for urgent patients
- Zero incomplete records due to time pressure
- No dangerous delays in patient handoff to triage

---

### JTBD-1.2: Work Effectively with Gloves

**Statement**: When processing patients while wearing gloves or with sanitized hands, I want to interact with the UI without removing gloves, so I can maintain infection control protocols and avoid workflow disruptions.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous throughout 12-hour shift) |
| Importance | High |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-1.3 |
| Related Gaps | GAP-002 (Touchscreen-optimized UI) |

**Job Steps**:
1. Put on gloves at start of shift or after patient contact
2. Interact with intake form (buttons, fields, checkboxes)
3. Complete intake without removing gloves
4. Maintain click accuracy >95%

**Success Criteria**:
- Large touch targets (minimum 60x60px for primary actions)
- Click accuracy >95% with gloves on
- Zero need to remove gloves for UI interaction
- Infection control compliance maintained

---

### JTBD-1.3: Use Keyboard Navigation Exclusively

**Statement**: When entering patient data during high-volume periods, I want to use tab-enter navigation exclusively, so I can process patients without touching the mouse and maximize speed.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-1.1 |
| Related Gaps | GAP-003 (Keyboard shortcuts) |

**Job Steps**:
1. Position hands on keyboard at start of intake
2. Tab through fields (Name → DOB → Complaint → Allergies)
3. Enter data via keyboard only
4. Submit form with Enter key
5. Never touch mouse during intake process

**Success Criteria**:
- Complete intake without using mouse
- Tab order is logical and matches workflow
- Enter key submits form immediately
- Keyboard shortcuts documented and discoverable

---

### JTBD-1.4: Escalate Trauma Cases Immediately

**Statement**: When a trauma patient arrives requiring immediate doctor attention, I want to bypass normal intake workflow with one click, so I can get the patient to clinical staff instantly without data entry delays.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (2-5 times/day, more during accidents/weekends) |
| Importance | Critical |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-1.1 |
| Related Gaps | GAP-004 (Trauma bypass button) |

**Job Steps**:
1. Identify trauma patient (car accident, gunshot, cardiac arrest)
2. Click giant red "Emergency Bypass" button
3. Minimal data capture (Name, DOB only)
4. Patient immediately routed to doctor
5. Complete intake details later

**Success Criteria**:
- Bypass button is giant, unmissable, red
- One-click action (no confirmation dialog)
- Bypass time <10 seconds
- Patient status immediately visible to doctor

---

### JTBD-1.5: Mark Patients Who Leave Without Being Seen

**Statement**: When a patient leaves the waiting room before being triaged, I want to mark them as "LWBS" (Left Without Being Seen) in one click, so I can prevent backlog confusion and maintain accurate queue status.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (3-8 times/day, more during long waits) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-1.2 |
| Related Gaps | GAP-005 (LWBS quick action) |

**Job Steps**:
1. Notice patient has left waiting room
2. Locate patient in queue
3. Click "LWBS" button
4. Patient removed from active queue
5. No confirmation dialog needed

**Success Criteria**:
- One-click LWBS action
- No confirmation dialog
- Patient immediately removed from triage queue
- Status visible to all staff

---

### JTBD-1.6: Work Comfortably During Night Shifts (Emotional)

**Statement**: When working night shifts in a dimly lit ER, I want to use a dark mode interface, so I can reduce eye strain and avoid screen brightness discomfort during 12-hour shifts.

| Attribute | Value |
|-----------|-------|
| Frequency | Weekly (night shift rotation) |
| Importance | Medium |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-4.1 |
| Related Gaps | GAP-006 (Dark mode) |

**Job Steps**:
1. Log in to system at night shift start (19:00-07:00)
2. Toggle dark mode manually or automatically (time-based)
3. Work entire shift with dark UI
4. Maintain readability and usability

**Success Criteria**:
- Dark mode available (manual toggle or automatic)
- Eye strain rating <3/10 for night shift staff
- All UI elements remain readable in dark mode
- No bright white flash when switching screens

---

## P-1.2: Triage Nurse (Carol) Jobs

### JTBD-2.1: Identify Next Patient Instantly

**Statement**: When I complete triage for one patient, I want to see the next patient in queue immediately without searching, so I can prevent bottlenecks and maintain efficient patient flow.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (40-60 times/shift) |
| Importance | High |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-1.2 |
| Related Gaps | GAP-007 (Auto-advance queue) |

**Job Steps**:
1. Complete current patient triage (vitals, ESI, notes)
2. Click "Triage Complete" button
3. Next patient automatically loads on screen
4. No clicking through menus or searching
5. Begin next triage immediately

**Success Criteria**:
- Auto-advance queue (next patient loads automatically)
- Zero navigation required between patients
- Triage time drops from 10+ minutes to <5 minutes
- Bottleneck elimination reported by staff

---

### JTBD-2.2: Capture Vitals Quickly with Gloves

**Statement**: When taking patient vitals while wearing gloves, I want to enter BP, HR, O2, and Temp values with large touch targets, so I can maintain infection control without slowing workflow.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous, 40-60 times/shift) |
| Importance | High |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-1.3 |
| Related Gaps | GAP-008 (Vitals entry - glove-friendly) |

**Job Steps**:
1. Take patient vitals (BP cuff, pulse ox, thermometer)
2. Wear gloves during data entry
3. Tap large input fields or buttons for each value
4. Submit vitals without removing gloves

**Success Criteria**:
- Large touch targets (60x60px minimum)
- Click accuracy >95% with gloves
- Vitals entry time <60 seconds
- Optional: Autofill from connected medical devices

---

### JTBD-2.3: Assign Initial ESI Level

**Statement**: When completing triage assessment, I want to assign an ESI (Emergency Severity Index) level using large, color-coded buttons, so I can quickly communicate patient acuity to the doctor.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous, 40-60 times/shift) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-1.2 |
| Related Gaps | GAP-009 (ESI level selector) |

**Job Steps**:
1. Assess patient condition during triage
2. Determine ESI level (1-5 scale)
3. Click corresponding ESI button (color-coded)
4. ESI level saved and visible to doctor

**Success Criteria**:
- Large 1-5 buttons (color-coded: Red, Orange, Yellow, Green, Blue)
- One-click assignment
- Visual confirmation of selected ESI
- Doctor can see ESI level immediately

---

### JTBD-2.4: Add Clinical Context for Doctor

**Statement**: When I observe concerning patient behavior or clinical indicators, I want to add free-text contextual notes, so the doctor has qualitative information beyond vitals and ESI scores.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (20-30 times/shift for concerning cases) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-5.2 |
| Related Gaps | GAP-010 (Clinical notes field) |

**Job Steps**:
1. Observe patient during triage (sweating, agitation, pain level)
2. Add free-text note in "Clinical Notes" field
3. Examples: "Patient sweating profusely, agitated behavior"
4. Note visible to doctor during evaluation

**Success Criteria**:
- Free-text field (optional)
- No character limit (reasonable length)
- Notes immediately visible to doctor
- Doctor satisfaction rating >90% with context quality

---

### JTBD-2.5: Onboard Float Staff Without Training

**Statement**: When regular staff are on vacation and float nurses arrive, I want them to use the system effectively within 30 seconds, so we don't experience workflow disruption or errors due to unfamiliarity.

| Attribute | Value |
|-----------|-------|
| Frequency | Weekly (vacation coverage, sick days) |
| Importance | High |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-4.3 |
| Related Gaps | GAP-011 (Zero-training UI) |

**Job Steps**:
1. Float nurse arrives (no prior system training)
2. Log in and begin triage immediately
3. Intuitive UI guides workflow (tooltips, logical layout)
4. Complete triage within 60 seconds (vs 45s for regular staff)

**Success Criteria**:
- Float staff can complete triage in <60s (vs 45s for regular staff)
- Intuitive UI (clear labels, logical flow)
- Zero training time available
- Error rate for float staff <5%

---

### JTBD-2.6: Work Comfortably During Night Shifts (Emotional)

**Statement**: When working night shifts in a dimly lit triage room, I want to use a dark mode interface, so I can reduce eye strain and avoid burning eyes after 12-hour shifts.

| Attribute | Value |
|-----------|-------|
| Frequency | Weekly (night shift rotation) |
| Importance | Medium |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-4.1 |
| Related Gaps | GAP-006 (Dark mode) |

**Job Steps**:
1. Log in to system at night shift start (19:00-07:00)
2. Toggle dark mode manually or automatically (time-based)
3. Work entire shift with dark UI
4. Maintain readability and usability

**Success Criteria**:
- Dark mode available (manual toggle or automatic)
- Eye strain rating <3/10 for night shift staff
- All UI elements remain readable in dark mode
- No bright white flash when switching screens

---

## P-1.3: Triage Doctor (Dr. Evans) Jobs

### JTBD-3.1: Maintain Full Manual Control Over Prioritization

**Statement**: When evaluating triaged patients, I want to manually assign wait time slots based on clinical judgment, so I can prevent automated systems from overriding critical medical decisions.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous throughout shift) |
| Importance | Critical |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-5.2 |
| Related Gaps | GAP-012 (Manual time slot assignment) |

**Job Steps**:
1. Review triaged patient (vitals, chief complaint, nurse notes)
2. Apply clinical judgment (visual cues, behavioral indicators)
3. Manually assign to time-based queue (Immediate, 30m, 60m, 120m, Rest)
4. NO automated escalation based on wait time alone

**Success Criteria**:
- 100% manual time slot assignment
- No automated escalation based on wait time
- Clinical judgment preserved
- Visual alerts at 110%/150% thresholds (not automatic escalation)

---

### JTBD-3.2: Visualize Patient Flow via Kanban Board

**Statement**: When managing patient flow throughout my shift, I want to see all patients organized in time-based columns, so I can prioritize evaluations and drag-and-drop patients as conditions change.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous) |
| Importance | Critical |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-3.2 |
| Related Gaps | GAP-013 (Kanban board interface) |

**Job Steps**:
1. View Kanban board: To Be Triaged, 30m, 60m, 120m, Rest, With Doctor
2. Review patient cards (age, chief complaint, vitals, ESI, notes)
3. Drag-and-drop patients between columns as conditions change
4. One-click time slot assignment (no right-click, no modifier keys)

**Success Criteria**:
- Kanban board with drag-and-drop
- Columns: To Be Triaged, 30m, 60m, 120m, Rest, With Doctor
- Patient cards show: Age, chief complaint, vitals, ESI, nurse notes
- One-click time slot buttons as alternative to drag-and-drop

---

### JTBD-3.3: See Real-Time Wait Time Alerts

**Statement**: When patients approach or exceed their assigned wait time thresholds, I want to receive visual alerts, so I can re-evaluate prioritization before conditions escalate.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (10-20 times/shift) |
| Importance | High |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-3.2 |
| Related Gaps | GAP-014 (Visual wait time alerts) |

**Job Steps**:
1. Monitor patient wait times in real-time
2. Receive visual alert when patient reaches 110% of assigned time (yellow border)
3. Receive escalated alert at 150% (red border)
4. Re-evaluate patient priority and adjust manually if needed

**Success Criteria**:
- Yellow alert at 110% of assigned wait time
- Red alert at 150% of assigned wait time
- Alerts trigger within 1 second of threshold breach
- Alerts do NOT automatically escalate patient (manual control only)

---

### JTBD-3.4: Update Public Display Instantly

**Statement**: When I assign or update a patient's wait time slot, I want the change to appear on the public waiting room display within 1 second, so patients don't confront staff due to perceived lag.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous, every patient update) |
| Importance | Critical |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-3.2 |
| Related Gaps | GAP-015 (Real-time WebSocket updates) |

**Job Steps**:
1. Assign patient to time slot (e.g., 30-minute wait)
2. Change propagates to public display via WebSocket
3. Patient sees updated status within 1 second
4. No patient confrontation due to display lag

**Success Criteria**:
- Display update latency <1 second
- Zero patient confrontations due to lag
- WebSocket-based updates (not polling)
- Real-time sync across all displays

---

### JTBD-3.5: Bulk Update Patients When Beds Open

**Statement**: When trauma beds become available, I want to select multiple "Immediate" patients and move them to "With Doctor" status at once, so I can efficiently manage patient flow during bed turnover.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (5-10 times/shift when beds open) |
| Importance | High |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-1.2 |
| Related Gaps | GAP-016 (Bulk update capability) |

**Job Steps**:
1. Receive notification that Trauma 1 or 2 bed is available
2. Select multiple patients in "Immediate" queue
3. Click "Move to With Doctor" bulk action
4. All selected patients updated simultaneously

**Success Criteria**:
- Multi-select patients (checkbox or Shift+click)
- Bulk update button (move to "With Doctor")
- Time to reassign patients reduced by 80%
- No confirmation dialog for bulk actions

---

### JTBD-3.6: Flag Patients for Security

**Statement**: When I identify a patient exhibiting aggressive or unpredictable behavior, I want to flag them for security coordination, so staff are aware of potential safety risks without displaying this on the public board.

| Attribute | Value |
|-----------|-------|
| Frequency | Weekly (2-5 times/week) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-5.2 |
| Related Gaps | GAP-017 (Behavioral risk flag) |

**Job Steps**:
1. Observe patient behavior during evaluation (agitation, verbal threats)
2. Add "Behavioral Risk" flag to patient record
3. Flag visible to staff only (red icon on internal views)
4. NOT visible on public display

**Success Criteria**:
- One-click behavioral risk flag
- Internal only (not on public display)
- Red icon visible on patient card
- Security notified via internal alert

---

### JTBD-3.7: Work on Desktop and Tablet Seamlessly

**Statement**: When moving between command center (desktop) and mobile triage (tablet), I want the same workflow and UI, so I don't have to learn device-specific interactions.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous, switching between desktop and tablet) |
| Importance | Medium |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-1.3 |
| Related Gaps | GAP-018 (Responsive design) |

**Job Steps**:
1. Use desktop at command center for patient flow overview
2. Use Surface tablet for mobile triage in patient rooms
3. Same workflow, same UI, same functionality
4. No device-specific training required

**Success Criteria**:
- Responsive design (desktop and tablet)
- Same workflow on both devices
- Touch-optimized for tablet (large targets)
- No device-specific training needed

---

## P-2.1: Patient Rights Representative (Linda) Jobs

### JTBD-4.1: Ensure Patients Recognize Their ID (Emotional)

**Statement**: When patients wait for triage or treatment, I want them to recognize their identifier on the public display, so they feel acknowledged and human rather than just a number.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous for all patients) |
| Importance | Critical |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-2.2 |
| Related Gaps | GAP-019 (Privacy-compliant patient IDs) |

**Job Steps**:
1. Patient receives identifier at intake (initials + day format: "LC-16")
2. Patient looks at public display and recognizes "LC-16"
3. Patient feels humanized and acknowledged (not "cattle")
4. Privacy preserved (no full names, GDPR/HIPAA compliant)

**Success Criteria**:
- Initials + day format (e.g., "LC-16" for Linda Chen on 16th)
- Patients recognize their ID immediately
- Patient satisfaction rating >4/5
- Zero complaints about feeling dehumanized

---

### JTBD-4.2: Reduce Patient Anxiety with Safe Wait Time Communication

**Statement**: When displaying wait times to patients, I want to use category-based messaging (e.g., "30-minute wait") instead of countdown timers, so patients don't become confrontational when times expire.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous) |
| Importance | Critical |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-5.1 |
| Related Gaps | GAP-020 (Category-based wait times) |

**Job Steps**:
1. Display patient ID with wait category ("30-minute wait", "60-minute wait")
2. NO countdown timers (no "59:59" ticking down)
3. Update status message when patient moves ("Waiting for Doctor", "With Doctor")
4. Prevent patient anxiety and confrontation

**Success Criteria**:
- Category-based wait times only (no countdown timers)
- Zero patient confrontations due to expired timers
- Patient satisfaction >4/5 for wait time communication
- Safe status message enum (no medical details)

---

### JTBD-4.3: Maintain Privacy Compliance on Public Display

**Statement**: When displaying patient status information, I want to ensure no GDPR or HIPAA violations occur, so the hospital avoids legal liability and protects patient privacy.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous) |
| Importance | Critical |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-2.1 |
| Related Gaps | GAP-019 (Privacy-compliant patient IDs) |

**Job Steps**:
1. Verify no full patient names on public display
2. Verify no medical details (chief complaint, vitals) on public display
3. Use safe status messages only ("Waiting for Triage", "Waiting for Doctor", "With Doctor")
4. Audit compliance regularly

**Success Criteria**:
- Zero GDPR/HIPAA violations detected
- No full patient names on public display
- No medical details on public display
- Safe status message enum enforced

---

### JTBD-4.4: Create Calming Visual Environment (Emotional)

**Statement**: When patients and families wait in the ER during night hours, I want the public display to use dark mode, so we reduce sensory overload in an already stressful environment.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (night hours: 19:00-07:00) |
| Importance | Medium |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-4.2 |
| Related Gaps | GAP-006 (Dark mode) |

**Job Steps**:
1. Public display automatically switches to dark mode at night (19:00)
2. Bright white screens dimmed to dark background with high-contrast text
3. Families with sick children experience less sensory overload
4. Display switches back to light mode in morning (07:00)

**Success Criteria**:
- Automatic time-based dark mode (19:00-07:00)
- High contrast maintained (readable from 20+ feet)
- Patient/family comfort improved
- Zero complaints about bright displays at night

---

### JTBD-4.5: Enable Family Tracking of Patient Progress (Social)

**Statement**: When family members wait in the lobby, I want them to track their loved one's progress via the patient ID, so they feel informed and reassured without violating privacy.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (continuous for all families) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-2.2 |
| Related Gaps | GAP-021 (Family tracking) |

**Job Steps**:
1. Family member knows patient ID (e.g., "LC-16")
2. Family watches public display for status updates
3. Sees status change: "Waiting for Triage" → "Waiting for Doctor" → "With Doctor"
4. Feels informed and reassured without needing staff intervention

**Success Criteria**:
- Family members can identify patient by initials+day ID
- Status updates visible in real-time
- High confidence in tracking patient progress
- No need for manual verbal updates from staff

---

## P-2.2: IT & Compliance Lead (Marcus) Jobs

### JTBD-5.1: Ensure System Works During Internet Outages

**Statement**: When internet connectivity is lost during storms or outages, I want the system to continue operating on the internal LAN, so we don't lose patient queue data or disrupt clinical workflow.

| Attribute | Value |
|-----------|-------|
| Frequency | Seasonal (storm-related, unpredictable) |
| Importance | Critical |
| Current Satisfaction | 1/5 |
| Related Pain Points | PP-3.1 |
| Related Gaps | GAP-022 (On-premise deployment) |

**Job Steps**:
1. Internet connection lost during storm
2. System continues operating on internal LAN (Ubuntu VMs, Docker)
3. Patient queue data preserved
4. Clinical staff continue normal workflow
5. No manual fallback to paper required

**Success Criteria**:
- 99.9% uptime on internal LAN
- Zero data loss during internet outages
- No cloud dependencies (CDNs, external APIs)
- All assets bundled in tarball (air-gapped deployment)

---

### JTBD-5.2: Deploy Updates Manually Without Vendor VPN

**Statement**: When a new system release is ready, I want to deploy it manually via tarball delivery, so I don't need to wait 2 weeks for vendor VPN approval.

| Attribute | Value |
|-----------|-------|
| Frequency | Monthly (update/patch cycles) |
| Importance | Medium |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-6.1 |
| Related Gaps | GAP-023 (Manual deployment) |

**Job Steps**:
1. Receive tarball from vendor (via secure file transfer)
2. Extract tarball on Ubuntu VM
3. Run Docker Compose down/up
4. Verify deployment (smoke tests)
5. Complete deployment in <15 minutes

**Success Criteria**:
- Deployment time <15 minutes
- Zero downtime (or <5 minutes)
- No vendor VPN required
- Docker Compose-based deployment

---

### JTBD-5.3: Enforce GDPR/HIPAA Compliance

**Statement**: When auditing system compliance, I want to verify patient data privacy controls, so we avoid legal liability and regulatory violations.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (compliance monitoring), Quarterly (formal audits) |
| Importance | Critical |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-2.1 |
| Related Gaps | GAP-019 (Privacy-compliant patient IDs) |

**Job Steps**:
1. Audit public display logs (no full patient names)
2. Verify 24-hour patient data deletion (GDPR)
3. Check LDAP authentication and role-based access (Clinical vs View-Only)
4. Review audit logs (30-day retention, anonymized patient IDs)

**Success Criteria**:
- Zero GDPR/HIPAA violations detected
- 100% audit compliance
- 24-hour patient data deletion enforced
- 30-day audit log retention

---

### JTBD-5.4: Manage LDAP Authentication and Role-Based Access

**Statement**: When onboarding new staff or assigning system access, I want to integrate with Active Directory for authentication and enforce role-based access control, so clinical staff have write access and public displays have view-only access.

| Attribute | Value |
|-----------|-------|
| Frequency | Weekly (new staff, role changes) |
| Importance | High |
| Current Satisfaction | 3/5 |
| Related Pain Points | PP-6.2 |
| Related Gaps | GAP-024 (LDAP authentication) |

**Job Steps**:
1. New staff member added to Active Directory
2. Assign role: Clinical (read/write) or View-Only (public display)
3. Staff logs in via LDAP
4. System enforces role-based access

**Success Criteria**:
- LDAP/Active Directory integration working
- Role-based access control enforced
- Clinical users: read/write
- View-Only users: public display only

---

### JTBD-5.5: Mitigate Session Timeout Data Loss

**Statement**: When staff are interrupted during data entry and the 15-minute session timeout occurs, I want partially completed forms to be autosaved, so staff don't lose work and have to re-enter data.

| Attribute | Value |
|-----------|-------|
| Frequency | Daily (especially during busy periods with interruptions) |
| Importance | Medium |
| Current Satisfaction | 2/5 |
| Related Pain Points | PP-6.2 |
| Related Gaps | GAP-025 (Autosave drafts) |

**Job Steps**:
1. Staff begins data entry (patient intake, vitals)
2. Interrupted by urgent patient or phone call
3. Autosave triggers every 30 seconds (draft saved locally)
4. Session timeout at 15 minutes
5. Staff logs back in and recovers draft

**Success Criteria**:
- Autosave every 30 seconds
- Session warning at 14 minutes ("You will be logged out in 1 minute")
- Draft recovery on re-login
- Zero data loss complaints from staff

---

## JTBD Summary by Priority

### Critical Jobs (Must Address)

| ID | Job | Persona | Pain Points |
|----|-----|---------|-------------|
| JTBD-1.1 | Process Urgent Patients Instantly | Intake Nurse | PP-1.1 |
| JTBD-1.4 | Escalate Trauma Cases Immediately | Intake Nurse | PP-1.1 |
| JTBD-3.1 | Maintain Full Manual Control Over Prioritization | Triage Doctor | PP-5.2 |
| JTBD-3.2 | Visualize Patient Flow via Kanban Board | Triage Doctor | PP-3.2 |
| JTBD-3.4 | Update Public Display Instantly | Triage Doctor | PP-3.2 |
| JTBD-4.1 | Ensure Patients Recognize Their ID | Patient Advocate | PP-2.2 |
| JTBD-4.2 | Reduce Patient Anxiety with Safe Wait Time Communication | Patient Advocate | PP-5.1 |
| JTBD-4.3 | Maintain Privacy Compliance on Public Display | Patient Advocate | PP-2.1 |
| JTBD-5.1 | Ensure System Works During Internet Outages | IT/Compliance | PP-3.1 |
| JTBD-5.3 | Enforce GDPR/HIPAA Compliance | IT/Compliance | PP-2.1 |

### High Priority Jobs

| ID | Job | Persona | Pain Points |
|----|-----|---------|-------------|
| JTBD-1.2 | Work Effectively with Gloves | Intake Nurse | PP-1.3 |
| JTBD-1.3 | Use Keyboard Navigation Exclusively | Intake Nurse | PP-1.1 |
| JTBD-1.5 | Mark Patients Who Leave Without Being Seen | Intake Nurse | PP-1.2 |
| JTBD-2.1 | Identify Next Patient Instantly | Triage Nurse | PP-1.2 |
| JTBD-2.2 | Capture Vitals Quickly with Gloves | Triage Nurse | PP-1.3 |
| JTBD-2.3 | Assign Initial ESI Level | Triage Nurse | PP-1.2 |
| JTBD-2.4 | Add Clinical Context for Doctor | Triage Nurse | PP-5.2 |
| JTBD-2.5 | Onboard Float Staff Without Training | Triage Nurse | PP-4.3 |
| JTBD-3.3 | See Real-Time Wait Time Alerts | Triage Doctor | PP-3.2 |
| JTBD-3.5 | Bulk Update Patients When Beds Open | Triage Doctor | PP-1.2 |
| JTBD-3.6 | Flag Patients for Security | Triage Doctor | PP-5.2 |
| JTBD-4.5 | Enable Family Tracking of Patient Progress | Patient Advocate | PP-2.2 |
| JTBD-5.4 | Manage LDAP Authentication and Role-Based Access | IT/Compliance | PP-6.2 |

### Medium Priority Jobs

| ID | Job | Persona | Pain Points |
|----|-----|---------|-------------|
| JTBD-1.6 | Work Comfortably During Night Shifts | Intake Nurse | PP-4.1 |
| JTBD-2.6 | Work Comfortably During Night Shifts | Triage Nurse | PP-4.1 |
| JTBD-3.7 | Work on Desktop and Tablet Seamlessly | Triage Doctor | PP-1.3 |
| JTBD-4.4 | Create Calming Visual Environment | Patient Advocate | PP-4.2 |
| JTBD-5.2 | Deploy Updates Manually Without Vendor VPN | IT/Compliance | PP-6.1 |
| JTBD-5.5 | Mitigate Session Timeout Data Loss | IT/Compliance | PP-6.2 |

---

## Traceability Matrix

| JTBD | Pain Points | Persona | Job Type |
|------|-------------|---------|----------|
| JTBD-1.1 | PP-1.1 | P-1.1 (Intake Nurse) | Functional |
| JTBD-1.2 | PP-1.3 | P-1.1 (Intake Nurse) | Functional |
| JTBD-1.3 | PP-1.1 | P-1.1 (Intake Nurse) | Functional |
| JTBD-1.4 | PP-1.1 | P-1.1 (Intake Nurse) | Functional |
| JTBD-1.5 | PP-1.2 | P-1.1 (Intake Nurse) | Functional |
| JTBD-1.6 | PP-4.1 | P-1.1 (Intake Nurse) | Emotional |
| JTBD-2.1 | PP-1.2 | P-1.2 (Triage Nurse) | Functional |
| JTBD-2.2 | PP-1.3 | P-1.2 (Triage Nurse) | Functional |
| JTBD-2.3 | PP-1.2 | P-1.2 (Triage Nurse) | Functional |
| JTBD-2.4 | PP-5.2 | P-1.2 (Triage Nurse) | Functional |
| JTBD-2.5 | PP-4.3 | P-1.2 (Triage Nurse) | Functional |
| JTBD-2.6 | PP-4.1 | P-1.2 (Triage Nurse) | Emotional |
| JTBD-3.1 | PP-5.2 | P-1.3 (Triage Doctor) | Functional |
| JTBD-3.2 | PP-3.2 | P-1.3 (Triage Doctor) | Functional |
| JTBD-3.3 | PP-3.2 | P-1.3 (Triage Doctor) | Functional |
| JTBD-3.4 | PP-3.2 | P-1.3 (Triage Doctor) | Functional |
| JTBD-3.5 | PP-1.2 | P-1.3 (Triage Doctor) | Functional |
| JTBD-3.6 | PP-5.2 | P-1.3 (Triage Doctor) | Functional |
| JTBD-3.7 | PP-1.3 | P-1.3 (Triage Doctor) | Functional |
| JTBD-4.1 | PP-2.2 | P-2.1 (Patient Advocate) | Emotional |
| JTBD-4.2 | PP-5.1 | P-2.1 (Patient Advocate) | Functional |
| JTBD-4.3 | PP-2.1 | P-2.1 (Patient Advocate) | Functional |
| JTBD-4.4 | PP-4.2 | P-2.1 (Patient Advocate) | Emotional |
| JTBD-4.5 | PP-2.2 | P-2.1 (Patient Advocate) | Social |
| JTBD-5.1 | PP-3.1 | P-2.2 (IT/Compliance) | Functional |
| JTBD-5.2 | PP-6.1 | P-2.2 (IT/Compliance) | Functional |
| JTBD-5.3 | PP-2.1 | P-2.2 (IT/Compliance) | Functional |
| JTBD-5.4 | PP-6.2 | P-2.2 (IT/Compliance) | Functional |
| JTBD-5.5 | PP-6.2 | P-2.2 (IT/Compliance) | Functional |

---

**Document Status**: Complete
**Next Phase**: Generate Product Vision and Strategy

*Generated by Discovery Skills Framework v5.0*
