---
document_id: PERSONA-Ragus-TRIAGE-NURSE
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: discovery-personas
source_files:
  - 01-analysis/ANALYSIS_SUMMARY.md
  - traceability/user_types_registry.json
  - traceability/pain_points_registry.json
---

# Persona: Triage Nurse (Carol)

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Carol Henderson |
| **Role** | Triage Nurse / Head Nurse |
| **Age** | 45 |
| **Experience** | 20+ years in emergency nursing |
| **Technical Proficiency** | Basic to intermediate |
| **Environment** | Triage room, wearing gloves, rotating day/night shifts |

## Profile

Carol is the head nurse responsible for taking patient vitals, assigning initial ESI (Emergency Severity Index) scores, and preparing patients for doctor evaluation. She's the critical link between intake and doctor assessment, and bottlenecks at her station can cascade throughout the ER.

> "I need to see who's next in line immediately when I finish with a patient. No clicking around, no searching. Just the next person, right there."

Carol works both day and night shifts and is a strong advocate for dark mode (her eyes hurt after 12-hour night shifts with bright screens). She also coordinates float staff during vacations and sick days, so the system must be intuitive enough that temporary nurses can use it without training.

## Goals with Success Metrics

| Goal | Success Metric | Current State |
|------|----------------|---------------|
| Complete triage efficiently without bottlenecks | Time from "Intake Complete" to "Triaged" <5 minutes | ~10+ minutes (workflow delays) |
| Provide accurate clinical context to doctors | Doctor satisfaction rating >90% | Manual notes, inconsistent format |
| Work effectively during night shifts | Eye strain rating <3/10, no brightness complaints | Bright white screens cause pain (PP-4.1) |
| Enable float staff to work without training | Float staff can complete triage in <60s (vs <45s for regular staff) | Buddy system, errors, delays (PP-4.3) |

## Pain Points (Linked to Registry)

### P1 - High Priority
- **[PP-1.2] Waiting room bottleneck between intake and triage**: Patients wait 10+ minutes between intake and triage, creating anxiety and inefficiency. Manual queue management is error-prone.
- **[PP-1.3] Poor UX for gloved/sanitized hands**: Clinical staff struggle with tiny UI elements and precise clicks while wearing gloves or with sanitized hands.
- **[PP-4.3] Zero training time requirement for float staff**: When regular staff are on vacation, float nurses must learn the system in <30 seconds or workflow breaks down.

### P2 - Medium Priority
- **[PP-4.1] Bright screens hurt night shift staff**: Bright white screens cause eye strain and discomfort during night shifts. No dark mode available.

> "At 3 AM, staring at that bright white screen feels like someone's shining a flashlight in my eyes."

## Daily Workflow

| Time | Activity | System Touchpoint | Pain Point |
|------|----------|-------------------|------------|
| 07:00 | Shift start, review patient queue | Login, view "Intake Complete" queue | Must see next patient immediately (PP-1.2) |
| 07:10-18:50 | Triage patients (continuous) | Vitals entry: BP, HR, O2, Temp; ESI score (1-5); Clinical notes | Gloved hands (PP-1.3), bottleneck if slow (PP-1.2) |
| Random | Float nurse arrives (vacation coverage) | Onboard temporary staff | Zero training time available (PP-4.3) |
| 19:00-07:00 | Night shift (rotates weekly) | Same workflow, night environment | Bright screens hurt eyes (PP-4.1) |

## Technical Context

- **Devices Used**: Desktop PC with touchscreen monitor, mouse/keyboard backup
- **Browser**: Chrome (kiosk mode)
- **Physical Constraints**: Wearing gloves, standing/sitting in triage room, interrupted frequently
- **Training Time**: Zero for float staff (must be intuitive)

## Jobs To Be Done (Preview)

When patients move from intake to triage, Carol needs to:
1. **Identify the next patient** in queue instantly without searching
2. **Capture vital signs** (BP, HR, O2, Temp) quickly and accurately
3. **Assign initial ESI level** (1-5 scale) based on clinical judgment
4. **Add contextual notes** for doctor review (e.g., "Patient sweating profusely, agitated behavior")
5. **Work comfortably during night shifts** without eye strain

## Representative Quotes

> "If I have to click through three screens to find the next patient, that's 30 seconds wasted per patient. Times 40 patients per shift, that's 20 minutes of just clicking around."

> "When Sarah goes on vacation and they send me a float nurse, I don't have time to train them. The system has to teach itself."

> "The bright white screen at night is torture. After 12 hours, my eyes are burning."

## Design Implications

### Must Have
- ✅ Auto-advance queue (next patient loads automatically after "Triage Complete")
- ✅ Large touch targets (60x60px minimum) for vitals entry
- ✅ ESI level selector (large 1-5 buttons, color-coded)
- ✅ Clinical notes field (free text, optional)
- ✅ Zero-training UI (intuitive for float staff in <30 seconds)

### Should Have
- ⭐ Dark mode (automatic time-based or manual toggle) - P2 priority
- ⭐ Vitals autofill from connected medical devices (BP cuff, pulse ox)
- ⭐ Behavioral risk flag (internal only, not on public display)

### Must NOT Have
- ❌ Multi-screen workflows (keep everything on one page)
- ❌ Hidden or nested menus
- ❌ Confirmation dialogs for routine actions

## Feature Priorities (Ranked)

1. **Auto-advance patient queue** (eliminate bottleneck) - P1
2. **Touchscreen-optimized vitals entry** (big buttons, glove-friendly) - P1
3. **Zero-training UI** (intuitive for float staff) - P1
4. **ESI level assignment** (large 1-5 buttons) - P1
5. **Clinical notes field** (context for doctor) - P1
6. **Dark mode** (night shift support) - P2

## Success Indicators

- Triage time drops from 10+ minutes to <5 minutes
- Float staff can complete triage within 60 seconds (vs 45s for regular staff)
- Night shift staff report <3/10 eye strain rating
- Zero workflow bottlenecks reported by triage staff

## Relationships

- **Receives From**: Intake Nurse (Jenny)
- **Reports To**: Shift Supervisor / ER Manager
- **Hands Off To**: Triage Doctor (Dr. Evans)
- **Coordinates With**: Float Staff (temporary coverage)
- **Serves**: Patients (triage phase)

## Related Artifacts

- **User Type**: UT-1.2 (Triage Nurse / Head Nurse)
- **Pain Points**: PP-1.2, PP-1.3, PP-4.1, PP-4.3
- **Source Facts**: CF-O-001, CF-O-002, CF-Q-003, CF-R-026, CF-Q-006, CF-R-023
- **Interview Sources**: Session_1.1_The_Clinical_Workflow.md, Session_2.1_Cross-Check___Validation.md
