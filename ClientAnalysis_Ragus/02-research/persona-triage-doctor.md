---
document_id: PERSONA-Ragus-TRIAGE-DOCTOR
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: discovery-personas
source_files:
  - 01-analysis/ANALYSIS_SUMMARY.md
  - traceability/user_types_registry.json
  - traceability/pain_points_registry.json
---

# Persona: Triage Doctor (Dr. Evans)

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Dr. Marcus Evans |
| **Role** | Emergency Physician / Triage Doctor |
| **Age** | 41 |
| **Experience** | 15 years in emergency medicine |
| **Technical Proficiency** | Intermediate |
| **Environment** | Mobile (tablet + desktop), high-pressure clinical setting |

## Profile

Dr. Evans is responsible for evaluating triaged patients and assigning wait time slots based on clinical judgment. He reviews patient vitals, chief complaints, and nurse notes, then manually assigns patients to time-based priority queues (Immediate, 30min, 60min, 120min, Rest).

> "I don't trust algorithms to make clinical decisions. If a patient is sweating profusely or acting agitated, that's a red flag I can see—but no computer algorithm will catch that."

Dr. Evans is adamantly opposed to automated time escalation systems. He needs full manual control over patient prioritization and visual alerts when wait times exceed clinical thresholds (yellow at 110%, red at 150%). He works on both desktop (command center) and tablet (Surface device for mobile triage).

## Goals with Success Metrics

| Goal | Success Metric | Current State |
|------|----------------|---------------|
| Maintain clinical control over patient prioritization | 100% manual time slot assignment, no automated escalation | Manual workarounds, spreadsheets |
| Quickly adjust patient flow as conditions change | Bulk update capability for multiple patients when beds open | Manual one-by-one updates |
| Identify escalating patient conditions via visual alerts | Yellow/red alerts trigger within 1 second of threshold breach | No real-time monitoring |
| Work efficiently on both desktop and tablet | Same workflow on desktop and Surface tablet | Separate systems, inconsistent UX |

## Pain Points (Linked to Registry)

### P0 - Critical
- **[PP-5.2] Automated escalation ignores clinical judgment**: Algorithms that automatically escalate patient priority based on wait time alone are dangerous. They cannot detect clinical indicators like profuse sweating, behavioral changes, or subtle deterioration that require human judgment.

> "If a computer automatically bumps someone to the front of the line because they've been waiting 2 hours, but they're stable and another patient is showing signs of sepsis, that's a recipe for disaster."

### P1 - High Priority
- **[PP-3.2] Display lag causes patient confrontation**: When Dr. Evans updates a patient's wait time, any delay in the public display update (even 1-2 seconds) causes patients to knock on the glass and confront staff. Real-time updates are essential.

## Daily Workflow

| Time | Activity | System Touchpoint | Pain Point |
|------|----------|-------------------|------------|
| 08:00 | Shift start, review patient queue | Login, open Kanban board (To Be Triaged, 30m, 60m, 120m, Rest) | Must see all patients at once |
| 08:15-19:45 | Evaluate triaged patients | Review vitals, chief complaint, nurse notes; Assign time slot | No automated escalation allowed (PP-5.2) |
| Random | Patient condition escalates | Visual alert (yellow at 110%, red at 150% of assigned wait time) | Must update time slot manually |
| Random | Bed becomes available (Trauma 1 or 2) | Bulk update: move multiple "Immediate" patients to "With Doctor" | One-by-one updates are slow |
| Random | Patient flagged for security | Add "Behavioral Risk" flag (internal only, not on public display) | Must be quick, no confirmation dialog |
| 20:00 | Shift handoff | Review outstanding patients with night shift doctor | N/A |

## Technical Context

- **Devices Used**: Desktop PC (command center), Surface tablet (mobile triage)
- **Browser**: Chrome (desktop), Edge (tablet)
- **Physical Constraints**: Mobile between triage room and trauma bays, often interrupted
- **Interaction Model**: Kanban board with drag-and-drop, one-click time slot buttons

## Jobs To Be Done (Preview)

When triaged patients are ready for evaluation, Dr. Evans needs to:
1. **Review patient vitals and clinical context** (vitals, chief complaint, nurse notes)
2. **Assign wait time slot** based on clinical judgment (Immediate, 30m, 60m, 120m, Rest)
3. **Monitor patient wait times** and receive visual alerts when thresholds are exceeded
4. **Bulk update patient status** when beds become available
5. **Flag patients for security** (behavioral risk, internal only)
6. **Re-categorize patients** as conditions change (escalate or de-escalate)

## Representative Quotes

> "I need a Kanban board. Show me columns: To Be Triaged, 30-minute, 60-minute, 120-minute, Rest. I drag and drop. Done."

> "When I assign a patient to the 30-minute queue, that needs to show up on the waiting room TV instantly. Not 5 seconds later. Instantly."

> "The algorithm doesn't know if a patient is about to crash. I do. That's why I'm the doctor."

## Design Implications

### Must Have
- ✅ Kanban board interface (columns: To Be Triaged, 30m, 60m, 120m, Rest)
- ✅ Drag-and-drop patient cards between columns
- ✅ One-click time slot buttons (no right-click, no modifier keys)
- ✅ Visual alerts: Yellow border at 110% wait time, Red border at 150%
- ✅ Bulk update capability (select multiple patients, move to "With Doctor")
- ✅ Real-time WebSocket updates (sub-second latency to public display)
- ✅ NO automated time escalation (100% manual control)

### Should Have
- ⭐ Patient details on card: Age, chief complaint, vitals, ESI level, nurse notes
- ⭐ Behavioral risk flag (internal only, red icon on card)
- ⭐ Responsive design (same UX on desktop and tablet)
- ⭐ Keyboard shortcuts (arrow keys + Enter for time slot assignment)

### Must NOT Have
- ❌ Automated time escalation based on wait time
- ❌ Confirmation dialogs for routine time slot changes
- ❌ Multi-step workflows for urgent actions (security flag, bulk updates)

## Feature Priorities (Ranked)

1. **Kanban board with drag-and-drop** (patient flow management) - P0
2. **Manual time slot assignment** (no automation) - P0
3. **Real-time WebSocket updates** (sub-second display sync) - P0
4. **Visual wait time alerts** (yellow at 110%, red at 150%) - P1
5. **Bulk update capability** (move multiple patients at once) - P1
6. **Behavioral risk flag** (security coordination) - P1
7. **Responsive design** (desktop + tablet) - P2

## Success Indicators

- 100% manual control over patient prioritization (no automated escalation)
- Display updates within 1 second of doctor action (zero patient confrontations due to lag)
- Bulk update capability reduces time to reassign patients by 80%
- Same workflow on desktop and tablet (no device-specific training)

## Relationships

- **Receives From**: Triage Nurse (Carol)
- **Reports To**: ER Medical Director
- **Coordinates With**: IT Manager (technical issues), Security (behavioral risk flags)
- **Serves**: Patients (evaluation and prioritization)

## Related Artifacts

- **User Type**: UT-1.3 (Triage Doctor)
- **Pain Points**: PP-5.2, PP-3.2
- **Source Facts**: CF-R-003, CF-R-004, CF-R-006, CF-R-007, CF-R-008, CF-R-010, CF-R-019, CF-R-025
- **Interview Sources**: Session_1.1_The_Clinical_Workflow.md, Session_2.1_Cross-Check___Validation.md
