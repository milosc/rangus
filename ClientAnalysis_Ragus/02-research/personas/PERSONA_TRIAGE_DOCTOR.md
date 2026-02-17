---
persona_id: P-1.3
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GeneratePersona
source_user_type: UT-1.3
---

# Persona: Dr. Michael "The Commander" Evans

**Archetype**: Triage Doctor
**Persona ID**: P-1.3
**Based on User Type**: UT-1.3 (Emergency Physician - Triage)

---

## Profile Summary

| Attribute | Value |
|-----------|-------|
| Name | Dr. Michael Evans |
| Nickname | "The Commander" |
| Age | 42 |
| Experience | 15 years as emergency physician, 8 years in triage role |
| Shift | Rotating (Days/Nights) |
| Primary Tool | Surface tablet (mobile) + Desktop workstation |
| Tech Comfort | High - Comfortable with technology but demands manual control over clinical decisions |

---

## Background

Dr. Evans is a 15-year veteran of emergency medicine, spending the last 8 years specializing in triage and patient flow management. He's known among staff as "The Commander" because of his decisive approach to prioritizing patients and managing the ER workflow. Michael understands that his time slot assignments (Immediate, 30min, 60min, 120min, Rest) are critical - they directly determine which patients receive care first and which must wait.

He's seen algorithmic systems fail by escalating patients based purely on wait time, ignoring clinical context. Michael trusts his judgment over any automated priority system. He knows that a stable patient who's been waiting 90 minutes might be safer than an anxious patient who arrived 10 minutes ago with vague symptoms. Clinical observation - profuse sweating, behavioral changes, skin color - can't be captured by algorithms.

Dr. Evans works between desktop and tablet (Surface), moving from the command center to trauma bays as needed. He values systems that give him complete manual control over patient prioritization, with visual alerts to flag patients approaching wait time thresholds. He doesn't want the system making decisions for him - he wants it highlighting situations that need his attention.

---

## A Day in Dr. Evans' Life

**07:00 AM** - Dr. Evans arrives for day shift, logs into the triage dashboard on desktop. He sees 12 patients triaged and awaiting time slot assignment. He quickly reviews vital signs, chief complaints, and nurse notes.

**07:15 AM** - First patient: 68-year-old male with chest pain, elevated BP. Dr. Evans assigns "Immediate" slot and flags for cardiac workup. Patient moves to top of queue.

**08:30 AM** - Kanban board shows 4 patients in "30min" column, 7 in "60min", 3 in "120min", 8 in "Rest". Patient in "60min" column has been waiting 55 minutes - visual alert shows yellow highlight (110% of assigned time). Dr. Evans reviews patient, decides to keep in current slot based on vital stability.

**10:15 AM** - Bed becomes available. Dr. Evans performs bulk update: moves 3 patients from "120min" to "60min", adjusts "30min" patient to "Immediate" based on worsening symptoms observed during waiting room monitoring.

**12:00 PM** - Moving to trauma bay with Surface tablet. Sees notification that patient flagged for security (behavioral risk noted by triage nurse). Reviews patient notes on tablet, confirms security presence needed before evaluation.

**02:45 PM** - Patient in "60min" column shows red alert (150% of assigned time). Dr. Evans reviews vitals and nurse notes - patient stable but frustrated. He reassigns to "30min" slot to prevent escalation.

**04:30 PM** - Reviewing waiting room public display on desktop. Sees his recent time slot update reflected on public board within 1 second - no delays, no patient confrontations at glass window. System latency is imperceptible.

**06:00 PM** - End of shift. Dr. Evans processed 47 patients through triage, adjusted 18 time slots based on clinical judgment, performed 3 bulk updates when beds became available. Zero algorithmic overrides - complete manual control maintained.

---

## Goals

### Primary Goals
1. **Maintain clinical control over patient prioritization** - Manual time slot assignment based on clinical judgment, not automated algorithms
2. **Quickly adjust patient flow as conditions change** - Bulk updates when beds open, individual re-prioritization when symptoms escalate
3. **Identify escalating patient conditions via visual alerts** - Yellow/red alerts for patients approaching wait time thresholds
4. **Work efficiently on both desktop and tablet** - Seamless workflow between command center (desktop) and mobile triage (Surface tablet)

### Secondary Goals
- Monitor patient wait times without constant manual checking
- Flag patients for security when behavioral risks are noted
- Re-categorize patients based on changing clinical conditions
- Prevent patient confrontations caused by display delays
- Perform bulk time slot adjustments when ER capacity changes

---

## Pain Points (Linked to Registry)

| Pain Point ID | Description | Impact on Dr. Evans |
|---------------|-------------|---------------------|
| PP-5.2 | Automated escalation ignores clinical judgment | Dangerous for patient safety - algorithms can't see profuse sweating, behavioral changes, or other clinical indicators that require human assessment |
| PP-3.2 | Display lag causes patient confrontation | When Dr. Evans updates time slots, any delay (even 1-2 seconds) causes patients to knock on glass and complain, disrupting workflow and creating staff stress |

---

## Frustrations

> "Algorithms can't see what I see. A patient who's been waiting 90 minutes with stable vitals is safer than someone who just arrived sweating profusely with vague chest discomfort. I need the system to alert me, not override me."

> "When I change a patient's wait time, it needs to update on the public display instantly. Even a 2-second delay causes patients to confront staff, thinking the system isn't working."

> "I don't want the system making clinical decisions. I want it showing me the data I need to make those decisions - vitals, wait times, alerts - and then getting out of my way."

---

## Motivations

- **Clinical Authority**: Dr. Evans is deeply committed to maintaining human clinical judgment over algorithmic automation. He's seen systems fail by escalating the wrong patients.
- **Patient Safety**: His prioritization decisions are life-or-death. He needs tools that support his judgment, not replace it.
- **Workflow Efficiency**: He wants to manage patient flow quickly and decisively, with visual tools (Kanban board, alerts) that highlight what needs attention.
- **Staff Protection**: He knows that display delays cause patient confrontations, which stress his nursing staff. He wants real-time updates to prevent these situations.

---

## Technology Profile

| Aspect | Current | Desired |
|--------|---------|---------|
| Device | Desktop (command center) + Surface tablet (mobile) | Same, with seamless sync between devices |
| Interface | Kanban board with drag-and-drop | Enhanced Kanban with visual alerts (yellow/red), bulk update tools |
| Training | Moderate training required | Intuitive drag-and-drop, minimal training for core functions |
| Customization | Fixed time slot categories | Custom time slots if needed, but defaults (30/60/120/Rest) work well |

### Technology Attitudes
- **Positive**: "I like visual tools like Kanban boards that let me see the whole ER at a glance. Drag-and-drop is fast and intuitive."
- **Skeptical**: "Any system that tries to make clinical decisions for me is dangerous. Algorithms don't understand context."
- **Pragmatic**: "Give me the data I need - vitals, wait times, alerts - and then let me make the call. That's what I'm trained for."

---

## Scenarios

### Scenario 1: Bulk Time Slot Update When Beds Open
**Current Experience**: 3 beds become available. Dr. Evans manually clicks each patient in "120min" column, opens edit dialog, changes time slot to "60min", clicks "Save". Repeats for all 6 patients. **Total: 4 minutes for 6 patients**

**Desired Experience**: 3 beds become available. Dr. Evans selects "BULK UPDATE" mode, selects 6 patients from "120min" column (checkbox selection), clicks "MOVE TO 60min" button. System updates all 6 instantly. **Total: 30 seconds for 6 patients**

### Scenario 2: Visual Alert for Exceeding Wait Time
**Current Experience**: Dr. Evans manually monitors each patient's wait time, checking timestamps against assigned slots. He discovers patient has exceeded 60-minute slot by 20 minutes only when staff alerts him verbally.

**Desired Experience**: Patient in "60min" column reaches 66 minutes (110% of assigned time). Card highlights in yellow automatically. At 90 minutes (150%), card turns red. Dr. Evans sees alerts instantly on Kanban board, reviews patient, makes prioritization decision.

### Scenario 3: Real-Time Public Display Update
**Current Experience**: Dr. Evans assigns patient to "30min" slot. Public display updates 2-3 seconds later due to polling delay. Patient sees old time category ("60min") on board, knocks on glass to complain. Staff has to explain system lag.

**Desired Experience**: Dr. Evans assigns patient to "30min" slot. Public display updates within 500ms via WebSocket push. Patient sees updated category immediately, no confusion, no confrontations.

---

## Design Implications

### Mobile UI Requirements
- **Responsive Kanban board** - Must work on both desktop (command center) and Surface tablet (mobile triage)
- **Visual alert system** - Yellow (110% of time), Red (150% of time), color-blind accessible with icons
- **One-click time slot buttons** - No right-click menus, no modifier keys
- **Drag-and-drop prioritization** - Move patients between columns (30m → 60m → 120m → Rest)
- **Patient detail cards** - Age, chief complaint, vital signs, nurse notes visible without drilling down

### Workflow Requirements
- **Manual-only time slot assignment** - No automated escalation or algorithm overrides
- **Bulk update mode** - Select multiple patients, apply time slot change to all
- **Security flagging** - One-click flag for patients requiring security presence
- **Re-categorization workflow** - Quick reassignment when symptoms escalate or stabilize
- **Real-time sync** - Sub-second latency for public display updates (WebSocket, not polling)

### Training Requirements
- **Intuitive Kanban interface** - Familiar mental model for workflow management
- **Contextual tooltips** - ESI guidelines, time slot definitions available on hover
- **Consistent drag-and-drop** - Same interaction pattern across all columns
- **Visual feedback** - Immediate confirmation when time slot changes are applied

---

## Quotes from Interviews

*From Session_1.1_The_Clinical_Workflow.md:*

> "Doctor: I don't want the system escalating patients automatically based on time alone. I need to see them, assess them, and make that call. Algorithms can't see profuse sweating or behavioral changes."

> "Question: What happens when you update a time slot? // Doctor: It needs to update on the public board instantly. Even a 1-2 second delay causes patients to knock on the glass thinking the system isn't working."

*From Session_2.1_Cross-Check___Validation.md:*

> "Doctor: I work between desktop at the command center and Surface tablet when I'm in trauma bays. I need the system to sync seamlessly between both."

---

## Traceability

| Link Type | IDs |
|-----------|-----|
| User Type | UT-1.3 |
| Pain Points | PP-5.2, PP-3.2 |
| Client Facts | CF-R-003, CF-R-004, CF-R-006, CF-R-007, CF-R-008, CF-R-010, CF-R-019, CF-R-025 |
| Gaps | None |

---

**Document Status**: Complete
**Next**: Generate JTBD for this persona
