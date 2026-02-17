---
persona_id: P-4.1
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GeneratePersona
source_user_type: UT-4.1
---

# Persona: Rachel "The Substitute" Kim

**Archetype**: Float Nurse / Temporary Staff
**Persona ID**: P-4.1
**Based on User Type**: UT-4.1 (Float Nurse)

---

## Profile Summary

| Attribute | Value |
|-----------|-------|
| Name | Rachel Kim |
| Nickname | "The Substitute" |
| Age | 29 |
| Experience | 5 years as float nurse across multiple departments |
| Shift | Variable (covers vacations, sick days, high-volume periods) |
| Primary Tool | Intake/Triage touchscreen workstations (unfamiliar systems) |
| Tech Comfort | Basic - Comfortable with simple interfaces, struggles with complex systems requiring training |

---

## Background

Rachel is a 29-year-old float nurse who covers shifts across multiple hospital departments - ER, ICU, Med-Surg, Pediatrics. She's been floating for 5 years, and she's learned to adapt quickly to unfamiliar environments. Rachel gets called in on short notice when regular staff are on vacation, out sick, or when patient volumes surge beyond normal capacity.

Rachel is known as "The Substitute" because she's the hospital's go-to solution when staffing gaps arise. She's competent and professional, but she faces a constant challenge: learning new systems with zero training time. When Rachel arrives for a shift in the ER triage area, she has **30 seconds** to figure out the interface before the next patient arrives. There's no time for manuals, no time for orientation, no time for mistakes.

Rachel has experienced both good and bad clinical systems. The good ones are self-explanatory - large labeled buttons, intuitive workflows, visual cues that guide her through processes without training. The bad ones are complex - nested menus, tiny text links, unclear navigation. When systems are poorly designed, Rachel makes errors, asks for help (interrupting busy staff), or avoids using features she doesn't understand.

---

## A Day in Rachel's Life

**06:15 AM** - Rachel receives text notification: "Need ER triage coverage today, 7 AM - 7 PM. Regular staff out sick. Can you cover?" Rachel confirms, arrives at hospital by 6:45 AM.

**06:50 AM** - Quick handoff from night shift head nurse (Carol). Carol shows Rachel the triage workstation: **"Here's the system. Click here to start triage, vitals go here, ESI level selector is here, clinical notes are here. Any questions?"** Rachel nods, but she's processing a lot of information at once. She has 10 minutes before first patient arrives.

**07:00 AM** - First patient called to triage. Rachel logs into system (LDAP credentials work - good). She sees main screen with large labeled sections: **"VITALS"**, **"ESI LEVEL"**, **"CLINICAL NOTES"**. Layout is self-explanatory. She starts capturing vital signs using large numeric keypad buttons (BP, HR, O2, Temp). Interface is glove-friendly - buttons are big enough to tap accurately.

**07:08 AM** - Rachel needs to assign ESI level. She sees visual scale (1-5) with color coding and brief descriptions. She selects ESI-3 (moderately urgent). System accepts input without errors. **Total triage time: 8 minutes.** Not perfect, but acceptable for first patient with zero training.

**08:30 AM** - Second patient. Rachel is getting faster - she's learned the workflow. Vitals capture, ESI selection, clinical notes. She notices preset templates for common observations ("Patient grimacing", "Appears anxious"). She uses them to save time instead of typing full sentences. **Total triage time: 6 minutes.**

**10:00 AM** - Third patient. Rachel accidentally taps wrong ESI button (ESI-2 instead of ESI-3). System shows large "UNDO" button at top of screen. She corrects error immediately. **No data loss, no need to ask for help.** She's impressed by the error recovery UX.

**12:00 PM** - Halfway through shift. Rachel has processed 12 patients without errors or need for help. She's confident with the interface now. She reflects: **"This is the first ER system I've used where I didn't have to call someone over to explain navigation."**

**03:30 PM** - Patient with complex allergy history. Rachel needs to enter detailed clinical notes. She finds text area clearly labeled "Clinical Notes (Internal - Not Visible on Public Display)". She types detailed observations, saves without issues.

**06:45 PM** - End of shift. Rachel processed 32 patients during 12-hour coverage. Zero errors, zero calls for help, zero workflow disruptions. She hands off to evening shift, feeling confident that she contributed effectively despite being unfamiliar with the system.

---

## Goals

### Primary Goals
1. **Understand system immediately without training** - Interface must be self-explanatory within 30 seconds of sitting down
2. **Avoid errors due to unfamiliarity** - Clear visual cues, large buttons, intuitive navigation prevent mistakes
3. **Maintain patient flow without disruption** - Float nurse should be as effective as regular staff within first hour of coverage

### Secondary Goals
- Complete triage tasks without asking for help (which interrupts busy staff)
- Avoid skipping features or workflows due to complexity or confusion
- Build confidence quickly so she can focus on patient care, not system navigation
- Minimize learning curve across different departments and systems

---

## Pain Points (Linked to Registry)

| Pain Point ID | Description | Impact on Rachel |
|---------------|-------------|------------------|
| PP-4.3 | Zero training time requirement for float staff | When Rachel covers ER shifts with no training, complex systems require constant help requests, leading to errors, workflow disruption, and reduced efficiency. |

---

## Frustrations

> "I've covered ER shifts where the triage system was so complex, I had to call the head nurse over 5 times during my first hour. That's embarrassing and it slows everyone down."

> "When I float to a new department, I don't have time for training. I sit down, and the next patient is already walking in. The system has to teach itself to me in real-time, or I'm going to make mistakes."

> "The worst systems have tiny text links, nested menus, and unclear button labels. I end up clicking things randomly just to see what happens. That's not safe for patients."

---

## Motivations

- **Professional Competence**: Rachel takes pride in being a reliable float nurse. She wants to perform effectively in any department, regardless of system familiarity.
- **Patient Safety**: She knows that errors caused by unfamiliar systems can impact patient care. She's motivated to use systems correctly, even under time pressure.
- **Efficiency**: Rachel wants to avoid slowing down workflows or interrupting busy staff with questions. She values systems that let her work independently.
- **Confidence**: She wants to feel confident using clinical systems, not anxious or uncertain about whether she's doing it right.

---

## Technology Profile

| Aspect | Current | Desired |
|--------|---------|---------|
| Device | Touchscreen workstations (variable by department) | Consistent, glove-friendly touchscreen interfaces |
| Interface | Varies from simple to complex | Self-explanatory, large labeled sections, visual cues |
| Training | Zero training time (30 seconds to learn on the fly) | Zero training required - intuitive within 30 seconds |
| Customization | None | Minimal customization needed - defaults work for 90% of cases |

### Technology Attitudes
- **Positive**: "I love systems with big buttons, clear labels, and visual cues. I can sit down and start using them immediately without asking for help."
- **Skeptical**: "Most clinical systems are designed for staff who use them every day. They forget about float nurses who cover 10 different departments with 10 different systems."
- **Pragmatic**: "If the interface isn't self-explanatory in 30 seconds, I'm either going to make mistakes or ask for help. Neither option is good for patients or staff."

---

## Scenarios

### Scenario 1: First Triage Patient with Zero Training
**Current Experience**: Rachel sits down at unfamiliar triage system. Interface has small text links, nested menus, unclear navigation. She clicks "Start Triage" but lands on wrong screen (patient search instead of vitals entry). She calls head nurse for help. Head nurse spends 3 minutes explaining workflow. **Total time lost: 3 minutes + patient wait time.**

**Desired Experience**: Rachel sits down at triage workstation. Interface shows large labeled sections: **"VITALS"**, **"ESI LEVEL"**, **"CLINICAL NOTES"**. She taps "VITALS", sees numeric keypad for BP/HR/O2/Temp. She captures vitals, moves to ESI selection (visual scale 1-5), adds clinical notes (text area), taps "COMPLETE TRIAGE". **Total time: 8 minutes for first patient, no help needed.**

### Scenario 2: Error Recovery Without Training
**Current Experience**: Rachel accidentally assigns wrong ESI level (ESI-2 instead of ESI-3). She doesn't see an "Undo" button. She asks staff: "How do I fix this?" Staff member has to log in, navigate to patient record, correct ESI level. **Total time lost: 5 minutes.**

**Desired Experience**: Rachel accidentally taps wrong ESI button. Large "UNDO" button appears at top of screen. She taps it immediately, corrects ESI level. **Total time: 5 seconds, no help needed.**

### Scenario 3: Using Advanced Features Without Training
**Current Experience**: Rachel needs to add detailed clinical notes (patient showing behavioral concerns). She finds small text field labeled "Notes". She types full paragraph, hits "Save", but system truncates notes to 100 characters. She loses work, has to retype in correct field. **Frustration and time lost.**

**Desired Experience**: Rachel needs to add clinical notes. She sees large text area clearly labeled "Clinical Notes (Internal - Not Visible on Public Display)". Character limit shown (500 chars). She types detailed observations, system auto-saves on blur. **No data loss, no confusion.**

---

## Design Implications

### Usability Requirements
- **Zero training design** - System must be self-explanatory within 30 seconds
- **Large labeled sections** - Clear visual hierarchy with section headers (VITALS, ESI LEVEL, NOTES)
- **Visual cues and icons** - Icons + text labels on all buttons
- **Glove-friendly touch targets** - 44x44px minimum button size
- **Consistent layout** - Same button positions across all screens

### Error Prevention & Recovery Requirements
- **Clear error messages** - No cryptic codes, explain what went wrong and how to fix it
- **Large "UNDO" buttons** - Easy error recovery without data loss
- **Auto-save on blur** - No manual "Save" button, data saved automatically when field loses focus
- **Confirmation for destructive actions** - "Are you sure?" dialogs for LWBS, delete, etc.

### Workflow Requirements
- **Single-screen workflows** - No multi-page wizards or hidden tabs
- **Preset templates** - Common clinical notes as one-click options ("Patient grimacing", "Appears anxious")
- **Tab navigation support** - Keyboard shortcuts for power users
- **Contextual tooltips** - Inline help for ESI guidelines, field definitions

---

## Quotes from Interviews

*From Session_2.1_Cross-Check___Validation.md:*

> "Question: What happens when regular staff are on vacation and float nurses cover? // Carol (Head Nurse): There's zero time for training. If they can't figure out the system in 30 seconds, they're going to struggle the whole shift or ask me for help every 10 minutes."

> "Float Nurse: The worst systems are the ones where I sit down and have no idea where to click. I need big buttons, clear labels, and visual cues. If it's not obvious, I'm either going to make mistakes or skip features I don't understand."

---

## Traceability

| Link Type | IDs |
|-----------|-----|
| User Type | UT-4.1 |
| Pain Points | PP-4.3 |
| Client Facts | CF-Q-006 |
| Gaps | None |

---

**Document Status**: Complete
**Next**: Generate JTBD for this persona
