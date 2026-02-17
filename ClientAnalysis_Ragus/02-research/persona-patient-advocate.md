---
document_id: PERSONA-Ragus-PATIENT-ADVOCATE
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: discovery-personas
source_files:
  - 01-analysis/ANALYSIS_SUMMARY.md
  - traceability/user_types_registry.json
  - traceability/pain_points_registry.json
---

# Persona: Patient Rights Representative (Linda)

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | Linda Chen |
| **Role** | Patient Rights Representative / Patient Advocate |
| **Age** | 38 |
| **Experience** | 12 years in patient advocacy |
| **Technical Proficiency** | Basic |
| **Environment** | Patient advocacy office, waiting room observation |

## Profile

Linda is responsible for ensuring the system treats patients humanely, reduces anxiety, and maintains dignity while preserving privacy. She advocates for patient-friendly display formats, humanized identification methods, and visual feedback that reassures patients rather than confusing or agitating them.

> "When you give a patient a number like '42', they feel like cattle. But when you use 'LC-16' (their initials and day), they recognize themselves immediately and feel human."

Linda has witnessed "patient riots" caused by countdown timers on public displays (patients watching timers tick down from 59:59 and becoming confrontational when time expires). She's a strong advocate for category-based wait times ("30-minute wait") instead of live countdowns.

## Goals with Success Metrics

| Goal | Success Metric | Current State |
|------|----------------|---------------|
| Reduce patient anxiety and feeling of being "cattle" | Patient satisfaction rating >4/5, zero complaints about dehumanization | Numeric tickets cause confusion, anxiety |
| Improve patient and family experience | Family members can track patient progress, understand status | Manual updates, verbal communication |
| Maintain dignity while preserving privacy | Privacy-compliant IDs, no GDPR/HIPAA violations | Full names displayed (non-compliant) |
| Create calming, informative display environment | Zero patient confrontations due to display confusion | Countdown timers cause "riots" (PP-5.1) |

## Pain Points (Linked to Registry)

### P0 - Critical
- **[PP-5.1] Countdown timers cause patient riots**: Displaying countdown timers (e.g., "59:59") on public boards causes extreme patient anxiety and confrontational behavior. Creates unsafe and stressful environment for staff and other patients.

> "We tried showing countdown timers once. Within 30 minutes, patients were banging on the glass, yelling at staff. It was chaos."

### P1 - High Priority
- **[PP-2.2] Patient anxiety with numeric-only identification**: Using only ticket numbers causes patients to forget their identifiers, lose paper slips, and feel dehumanized. Initials + day format (LC-16) balances privacy and recognition.

### P2 - Medium Priority
- **[PP-4.2] Aggressive bright public displays at night**: Bright white TV displays in waiting rooms at night (3 AM) are aggressive and uncomfortable for waiting patients and families in dim environments.

## Daily Workflow

| Time | Activity | System Touchpoint | Pain Point |
|------|----------|-------------------|------------|
| 09:00 | Review overnight patient complaints | Read incident reports, review public display logs | Identify usability issues causing anxiety |
| 10:00 | Observe waiting room experience | Watch public display, monitor patient reactions | Countdown timers cause confrontations (PP-5.1) |
| 11:00 | Collaborate with UX team | Define patient-friendly display formats (initials+day, status messages) | Balance privacy with humanization (PP-2.2) |
| Random | Respond to patient complaints | Explain wait times, provide updates | Manual intervention needed when display is confusing |
| 15:00 | Review compliance with GDPR lead | Ensure no patient names or medical details on public display | Privacy violations (PP-2.1) |

## Technical Context

- **Devices Used**: Laptop (monitoring public display screenshots), tablet (waiting room observation)
- **Browser**: Chrome
- **Physical Constraints**: None (office-based)
- **Interaction Model**: Read-only public display monitoring, policy definition

## Jobs To Be Done (Preview)

When patients wait for triage and treatment, Linda needs to:
1. **Ensure patients can recognize their ID** (initials + day format, not ticket numbers)
2. **Reduce anxiety** by showing category-based wait times (not live countdowns)
3. **Provide status clarity** with safe, informative messages ("Waiting for Doctor", not medical details)
4. **Create calming visual environment** (dark mode at night, high contrast, large fonts)
5. **Enable family tracking** (family members can identify patient by initials+day ID)

## Representative Quotes

> "If you show '59:59' on the screen, patients watch it like a hawk. When it hits zero and they're still waiting, they lose their minds."

> "Initials plus day-of-month is the sweet spot. 'LC-16' tells Linda Chen on the 16th that she's being tracked, but it doesn't violate GDPR."

> "At 3 AM, that bright white TV screen feels like a spotlight. Families with sick kids are already stressed—we shouldn't make it worse."

## Design Implications

### Must Have
- ✅ Privacy-compliant patient IDs (initials + day format: "LC-16")
- ✅ Category-based wait times ("30-minute wait", "60-minute wait") - NO countdown timers
- ✅ Safe status message enum ("Waiting for Triage", "Waiting for Doctor", "With Doctor", "Results Pending")
- ✅ High contrast, large fonts (readable from 20+ feet)
- ✅ Color-blind accessible (icons + text, not color alone)

### Should Have
- ⭐ Dark mode for night/dim environments (automatic time-based)
- ⭐ Visual feedback for patient status changes (blinking, highlighting when updated)
- ⭐ Collision handling for patient IDs (if two "LC-16" patients, add suffix: "LC-16a", "LC-16b")

### Must NOT Have
- ❌ Countdown timers (causes patient riots)
- ❌ Full patient names (GDPR/HIPAA violation)
- ❌ Medical details (chief complaint, vitals) on public display
- ❌ Numeric-only IDs (dehumanizing, forgettable)

## Feature Priorities (Ranked)

1. **Privacy-compliant patient IDs** (initials + day) - P0
2. **Category-based wait times** (no countdown timers) - P0
3. **Safe status message enum** (no medical details) - P1
4. **High contrast, large fonts** (accessibility) - P1
5. **Dark mode** (night display comfort) - P2
6. **Visual feedback for updates** (blinking, highlighting) - P2

## Success Indicators

- Zero patient confrontations due to countdown timers
- Patient satisfaction rating >4/5 for wait time communication
- Zero GDPR/HIPAA violations on public display
- Family members report high confidence in tracking patient progress

## Relationships

- **Reports To**: Hospital Administration / Patient Experience Director
- **Coordinates With**: Compliance Officer (GDPR/HIPAA), UX Specialist, Clinical Staff
- **Advocates For**: Patients, Families

## Related Artifacts

- **User Types**: UT-3.1 (Patient), UT-3.2 (Patient Rights Representative)
- **Pain Points**: PP-5.1, PP-2.2, PP-4.2
- **Source Facts**: CF-Q-004, CF-Q-005, CF-R-011, CF-R-012, CF-C-003, CF-R-015, CF-R-020, CF-R-024
- **Interview Sources**: Session_1.2_The_Privacy___Compliance_Barrier.md_, Session_2.1_Cross-Check___Validation.md
