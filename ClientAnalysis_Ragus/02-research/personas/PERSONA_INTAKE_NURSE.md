---
persona_id: P-1.1
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GeneratePersona
source_user_type: UT-1.1
---

# Persona: Jenny "The Gatekeeper" Rodriguez

**Archetype**: Intake Nurse
**Persona ID**: P-1.1
**Based on User Type**: UT-1.1 (Intake Nurse)

---

## Profile Summary

| Attribute | Value |
|-----------|-------|
| Name | Jenny Rodriguez |
| Nickname | "The Gatekeeper" |
| Age | 32 |
| Experience | 8 years in emergency nursing |
| Shift | Rotating (Days/Evenings) |
| Primary Tool | Touchscreen workstation at Intake Desk |
| Tech Comfort | Medium - Comfortable with clinical systems but frustrated by poor UX |

---

## Background

Jenny has been an ER nurse for 8 years, spending the last 4 years at the Intake Desk. She's the first person every patient meets when they arrive at the emergency room - a role she takes seriously. Jenny knows that her speed directly impacts patient outcomes, especially when trauma cases arrive.

She's developed lightning-fast assessment skills, able to identify urgent cases within seconds of seeing a patient. However, she's constantly battling with slow data entry systems that force her to type detailed information when she should be moving patients through to triage. Jenny often works with gloved hands after patient contact or with freshly sanitized hands, making touchscreen interaction challenging.

Her biggest frustration is being the bottleneck when she knows the system could help her go faster. She's seen colleagues struggle with training on complex systems, and she values tools that "just work" without requiring a manual.

---

## A Day in Jenny's Life

**07:00 AM** - Jenny arrives for the day shift, logs into the Intake system, and reviews overnight patient load. She sanitizes her hands and puts on gloves, preparing for direct patient contact.

**07:30 AM** - First patient arrives: elderly man with chest pain. Jenny needs to process him FAST - she captures name, DOB, chief complaint ("chest pain"), and allergies in under 30 seconds using large touch buttons. System creates "Intake Complete" state and patient moves to waiting room.

**09:45 AM** - Rush of patients after a multi-car accident. Trauma bypass alert - Jenny hits the emergency button to flag incoming trauma. She processes 3 walking wounded patients in under 2 minutes each, but the system's small text fields and tiny clickable links slow her down. She has to remove gloves twice to tap small UI elements accurately.

**12:30 PM** - Patient marked as LWBS (Left Without Being Seen) - she uses the system to update status so the triage nurse knows not to call this patient. Simple workflow, but requires precise clicks.

**02:15 PM** - Float nurse covering break asks Jenny how to mark a patient LWBS. Jenny explains in 15 seconds, and the float nurse completes it without issues. Jenny appreciates that the system is intuitive enough for untrained staff.

**04:00 PM** - End of shift. Jenny logged 47 patients today with an average intake time of 38 seconds - meeting the <60 second target for all but the most complex cases.

---

## Goals

### Primary Goals
1. **Process urgent patients in under 30 seconds** - Every second counts when a patient presents with chest pain, trauma, or stroke symptoms
2. **Minimize typing without sacrificing data accuracy** - Capture critical information (name, DOB, complaint, allergies) with minimal keystrokes
3. **Prevent intake bottlenecks** - Keep the queue moving so patients don't experience excessive wait times before triage

### Secondary Goals
- Work efficiently with gloved or sanitized hands without removing PPE frequently
- Enable float staff to operate the system without training
- Maintain data quality while working at maximum speed
- Avoid data entry errors that could impact patient safety

---

## Pain Points (Linked to Registry)

| Pain Point ID | Description | Impact on Jenny |
|---------------|-------------|-----------------|
| PP-1.1 | Slow patient intake during high-urgency situations | Forces Jenny to choose between speed and data completeness, creates dangerous delays for urgent patients |
| PP-1.3 | Poor UX for gloved/sanitized hands | Requires removing gloves frequently to tap small UI elements, slows workflow, potential infection control issues |

---

## Frustrations

> "When someone walks in with chest pain, I don't have time to type out their full medical history. I need name, birthdate, complaint, allergies - that's it. Every second I waste typing is a second that patient isn't getting to triage."

> "These tiny text links and little checkboxes are impossible to hit when you're wearing gloves or have sanitized hands. I'm constantly removing gloves just to click something, which defeats the whole purpose of infection control."

> "I've seen float nurses completely freeze up with complex systems during busy shifts. If they can't figure it out in 30 seconds, they're just going to skip it or ask me, which slows everyone down."

---

## Motivations

- **Patient Safety First**: Jenny knows that intake speed directly impacts patient outcomes. Delays at her desk can mean the difference between life and death for critical patients.
- **Efficiency Under Pressure**: She takes pride in processing patients quickly and accurately, maintaining calm during high-stress situations.
- **Team Support**: Jenny wants to make the system easy enough that float staff can cover her desk without training, ensuring continuity of care.

---

## Technology Profile

| Aspect | Current | Desired |
|--------|---------|---------|
| Device | Desktop touchscreen (20" monitor) | Same, but with glove-friendly UI |
| Interface | Text-heavy forms with small inputs | Large touch targets, minimal typing, tab navigation |
| Training | 2-hour formal training required | Zero training - intuitive within 30 seconds |
| Customization | None | Preset templates for common complaints |

### Technology Attitudes
- **Positive**: "I like systems that get out of my way and let me focus on the patient. Big buttons, fast forms, no unnecessary clicks."
- **Skeptical**: "Most EHR systems are designed by people who've never worked a shift in an ER. They don't understand that we need speed, not features."
- **Pragmatic**: "If it saves me 5 seconds per patient, that's 4 minutes per shift. That could be a life saved."

---

## Scenarios

### Scenario 1: Urgent Chest Pain Patient
**Current Experience**: Patient presents with chest pain. Jenny logs into system, clicks through 3 screens to create new patient, types full name (15 seconds), clicks DOB picker (10 seconds), selects gender from dropdown (5 seconds), types chief complaint in text area (15 seconds), clicks "Allergies" field and types details (10 seconds), clicks "Save" and "Send to Triage" (5 seconds). **Total: 60 seconds**

**Desired Experience**: Patient presents with chest pain. Jenny taps large "NEW PATIENT" button, speaks or quickly types name (autocomplete suggests matches), taps DOB (numeric keypad with large buttons), taps gender icon, taps "Chest Pain" from preset complaint buttons, taps "No Known Allergies" button, taps "COMPLETE INTAKE" large button. **Total: 25 seconds**

### Scenario 2: Processing During Trauma Alert
**Current Experience**: Multiple patients arrive after car accident. Jenny has to process each individually through the same slow form. She removes gloves 3 times to tap small "Save" buttons and text field selectors. **Total: 6 minutes for 4 patients**

**Desired Experience**: Jenny activates "TRAUMA MODE" - system switches to rapid-entry form with large touch targets designed for gloved hands. She processes all 4 patients without removing gloves, using preset buttons for common trauma complaints. **Total: 3 minutes for 4 patients**

### Scenario 3: Float Nurse Covering Break
**Current Experience**: Float nurse asks Jenny for 5-minute training on how to mark patients LWBS and how to navigate forms. Float nurse makes 2 errors clicking wrong buttons during first hour.

**Desired Experience**: Float nurse sits down, sees large labeled buttons ("NEW PATIENT", "MARK LWBS", "TRAUMA ALERT"). Interface is self-explanatory. No training needed - float nurse completes tasks without errors.

---

## Design Implications

### Mobile UI Requirements
- **Touch targets MUST be 44x44px minimum** - Large enough for gloved fingers to tap accurately
- **High-contrast buttons with clear labels** - No tiny text links or low-contrast UI elements
- **Voice input option for names/complaints** - Reduce typing when hands are occupied
- **Preset complaint buttons** - Common complaints (Chest Pain, Fall, Abdominal Pain, etc.) as one-tap options
- **Tab navigation support** - Keyboard shortcuts for power users who prefer keyboard

### Workflow Requirements
- **Minimize required fields** - Name, DOB, Gender, Complaint, Allergies - nothing more for basic intake
- **One-screen intake form** - No multi-page wizards or hidden tabs
- **Auto-save on field change** - No manual "Save" button required
- **LWBS workflow** - Single large button to mark patient left without being seen
- **Trauma bypass shortcut** - Emergency button accessible from any screen

### Training Requirements
- **Zero formal training** - System must be self-explanatory within 30 seconds
- **Visual cues** - Icons + text labels on all buttons
- **Consistent button placement** - Same location across screens for common actions
- **Inline help tooltips** - Context-sensitive help without leaving screen

---

## Quotes from Interviews

*From Session_1.1_The_Clinical_Workflow.md:*

> "Question: What's your target time for intake completion? // Jenny: Under 60 seconds for standard patients, under 30 for urgent. That's from patient arrival to clicking 'Intake Complete'."

> "When I'm wearing gloves or just sanitized my hands, clicking tiny UI elements is a nightmare. Everything needs to be big and obvious."

> "If float staff can't figure out the system in 30 seconds, they're going to call me over, and that defeats the purpose."

---

## Traceability

| Link Type | IDs |
|-----------|-----|
| User Type | UT-1.1 |
| Pain Points | PP-1.1, PP-1.3 |
| Client Facts | CF-Q-001, CF-R-001, CF-R-002, CF-Q-002, CF-R-009 |
| Gaps | None |

---

**Document Status**: Complete
**Next**: Generate JTBD for this persona
