---
document_id: PERSONA-Ragus-INTAKE-NURSE
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: discovery-personas
source_files:
  - 01-analysis/ANALYSIS_SUMMARY.md
  - traceability/user_types_registry.json
  - traceability/pain_points_registry.json
---

# Persona: Intake Nurse (Jenny)

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Jenny Martinez |
| **Role** | Intake Nurse / Front Desk Registration |
| **Age** | 32 |
| **Experience** | 8 years in emergency nursing |
| **Technical Proficiency** | Basic to intermediate |
| **Environment** | High-stress ER intake desk, often wearing gloves |

## Profile

Jenny is the first point of contact for every patient arriving at the ER. She works 12-hour shifts split between days and nights, and her primary responsibility is to get patients "into the system" as quickly as possible—especially when someone arrives in critical condition.

> "When a trauma comes in, I don't have time to type out long sentences. I need name, DOB, complaint, and done. 30 seconds max."

Jenny frequently wears gloves or has sanitized hands that don't work well with touchscreens. She needs large touch targets and keyboard shortcuts. During high-volume periods (flu season, weekends), she may process 40-60 patients per shift.

## Goals with Success Metrics

| Goal | Success Metric | Current State |
|------|----------------|---------------|
| Process urgent patients in under 30 seconds | Time from arrival to "Intake Complete" state | ~60-90 seconds (typing delays) |
| Minimize typing while maintaining accuracy | Error rate <2%, fields completed 100% | Manual workarounds, incomplete records |
| Prevent intake bottlenecks | Wait time from arrival to triage <5 minutes | ~10+ minutes during peaks |
| Work effectively with gloves/sanitized hands | Click accuracy >95%, no need to remove gloves | Frequent glove removal, stylus use |

## Pain Points (Linked to Registry)

### P0 - Critical
- **[PP-1.1] Slow patient intake during high-urgency situations**: Typing detailed information creates dangerous delays for urgent patients. Current workaround is minimal data entry leading to incomplete records.

### P1 - High Priority
- **[PP-1.3] Poor UX for gloved/sanitized hands**: Tiny UI elements and text links force her to remove gloves frequently, creating infection control issues and slowing workflow.

> "I can't click those little blue text links with gloves on. I end up ripping them off, then I have to sanitize again."

## Daily Workflow

| Time | Activity | System Touchpoint | Pain Point |
|------|----------|-------------------|------------|
| 07:00 | Shift start, log in to system | LDAP authentication | Session timeout at 07:15 if idle (PP-6.2) |
| 07:05-19:00 | Patient intake (continuous) | Intake screen: Name, DOB, Complaint, Allergies | Typing delays (PP-1.1), poor touch targets (PP-1.3) |
| Random | Trauma bypass alert | Red "Emergency Bypass" button | Needs to be giant, unmissable |
| Random | Patient leaves without being seen | Mark as "LWBS" (Left Without Being Seen) | Must be fast, no confirmation dialogs |
| 19:00 | Shift handoff | Review queue with night shift | N/A |

## Technical Context

- **Devices Used**: Desktop PC with touchscreen monitor (or mouse/keyboard), tablet for trauma bays
- **Browser**: Chrome (kiosk mode for dedicated stations)
- **Physical Constraints**: Wearing gloves, standing/sitting at desk, often interrupted
- **Training Time**: Zero for float staff (PP-4.3)

## Jobs To Be Done (Preview)

When patients arrive at the ER, Jenny needs to:
1. **Register them quickly** so they can proceed to triage without delay
2. **Capture essential medical information** (allergies, chief complaint) to prevent safety issues
3. **Handle urgent cases** with minimal friction (trauma bypass button)
4. **Mark patients as LWBS** when they leave to prevent backlog confusion

## Representative Quotes

> "During a car accident, I might get three patients at once. I need to get them all registered in under two minutes total."

> "The system we had before had tiny checkboxes. With gloves, I'd click the wrong one half the time."

> "If the keyboard shortcuts work, I never need to touch the mouse. That's the dream."

## Design Implications

### Must Have
- ✅ Large touch targets (minimum 44x44px, prefer 60x60px for primary actions)
- ✅ Tab-enter navigation (keyboard-first workflow)
- ✅ Minimal required fields (Name, DOB, Complaint only)
- ✅ Giant red "Emergency Bypass" button for trauma alerts
- ✅ One-click "LWBS" action (no confirmation dialog)

### Should Have
- ⭐ Autocomplete for common complaints ("Chest pain", "Fall", "Abdominal pain")
- ⭐ Voice input option for hands-free operation
- ⭐ Dark mode for night shifts (PP-4.1)

### Must NOT Have
- ❌ Required fields beyond Name/DOB/Complaint (slows urgent intake)
- ❌ Small text links or icons
- ❌ Confirmation dialogs for routine actions (LWBS, bypass)

## Feature Priorities (Ranked)

1. **Fast intake form** (Name, DOB, Complaint) - P0
2. **Touchscreen-optimized UI** (big buttons, glove-friendly) - P0
3. **Keyboard shortcuts** (tab-enter navigation) - P1
4. **Trauma bypass button** (emergency escalation) - P1
5. **LWBS quick action** (one-click status change) - P1
6. **Dark mode** (night shift support) - P2

## Success Indicators

- Intake time for urgent patients drops from 60-90s to <30s
- Glove removal frequency drops by 80%+
- Float staff can operate system within 30 seconds (no training)
- Zero incomplete intake records due to time pressure

## Relationships

- **Reports To**: Head Nurse / Shift Supervisor
- **Hands Off To**: Triage Nurse (Carol)
- **Coordinates With**: Triage Doctor (for trauma bypasses), IT Manager (for technical issues)
- **Serves**: Patients (all arrivals)

## Related Artifacts

- **User Type**: UT-1.1 (Intake Nurse)
- **Pain Points**: PP-1.1, PP-1.3
- **Source Facts**: CF-Q-001, CF-R-001, CF-R-002, CF-Q-002, CF-R-009
- **Interview Sources**: Session_1.1_The_Clinical_Workflow.md
