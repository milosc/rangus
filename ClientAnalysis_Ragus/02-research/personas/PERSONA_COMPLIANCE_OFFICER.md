---
persona_id: P-2.2
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GeneratePersona
source_user_type: UT-2.2
---

# Persona: Dr. Sarah "The Guardian" Halloway

**Archetype**: Compliance Officer (GDPR/HIPAA Lead)
**Persona ID**: P-2.2
**Based on User Type**: UT-2.2 (Compliance Officer)

---

## Profile Summary

| Attribute | Value |
|-----------|-------|
| Name | Dr. Sarah Halloway |
| Nickname | "The Guardian" |
| Age | 51 |
| Experience | 25 years in healthcare administration, 10 years focused on privacy/compliance |
| Shift | Standard business hours (8 AM - 5 PM), on-call for compliance incidents |
| Primary Tool | Compliance audit logs, policy documentation, legal review tools |
| Tech Comfort | Intermediate - Policy-focused, understands technical implications of compliance requirements |

---

## Background

Dr. Halloway has spent 25 years in healthcare administration, with the last 10 years dedicated to privacy and compliance. She's the hospital's GDPR and HIPAA lead, responsible for ensuring every system, process, and display meets strict regulatory requirements. Sarah is known as "The Guardian" because she protects patient privacy with unwavering vigilance - no shortcuts, no exceptions, no "we'll fix it later."

She's seen privacy violations destroy careers and cost hospitals millions in fines. She's reviewed countless vendor systems that displayed full patient names on public boards, stored sensitive medical data indefinitely, or failed to implement proper anonymization. Sarah's philosophy is simple: "Privacy isn't negotiable. If the system can't comply, it can't go live."

Dr. Halloway works closely with IT and clinical teams to define privacy-compliant workflows. She specifies patient ID formats (Initials + Day, under 8 characters), approves status message enums for public displays, defines data retention policies (30 days for logs, 24-hour deletion for patient data), and handles collision resolution when two patients share initials and arrive on the same day. She also reviews audit logging and anonymization practices to ensure compliance with GDPR and HIPAA requirements.

---

## A Day in Dr. Halloway's Life

**08:00 AM** - Dr. Halloway arrives at office, reviews overnight compliance audit logs. Checks for any privacy violations or unusual data access patterns. All clean.

**09:30 AM** - Meeting with vendor (triage system pilot). Vendor proposes displaying full patient names on public waiting room board. Dr. Halloway immediately rejects proposal, explains GDPR/HIPAA privacy requirements. Specifies privacy-compliant alternative: Initials + Day format (e.g., "JS-12" for John Smith on December 12th).

**10:45 AM** - Reviewing proposed status messages for public display. Vendor wants to show "Severe Chest Pain" as complaint. Dr. Halloway strikes it down - no medical details allowed on public boards. Approves safe enum: "Waiting for Triage", "Waiting for Doctor", "With Doctor", "Results Pending". No clinical information.

**12:00 PM** - IT manager asks about data retention policy. Dr. Halloway specifies: 30 days for audit logs (compliance requirement), 24-hour deletion for patient data post-disposition (GDPR minimization principle). No long-term storage of names, complaints, or vitals.

**02:15 PM** - Collision scenario: Two patients with initials "JS" arrive on same day (December 12th). Both would have ID "JS-12". Dr. Halloway defines resolution protocol: append sequential number (JS-12-1, JS-12-2), maximum 8 characters for display constraints.

**03:30 PM** - Auditing vendor anonymization implementation. Reviews code for patient ID generation, verifies no PHI (Protected Health Information) is logged in application logs or database audit trails. Finds log statement exposing patient name in error message - flags for immediate fix.

**04:45 PM** - Final review of public display mockup. Verifies no names, no medical details, no birthdates visible. Approves design with condition: font size must be large enough to read from 20 feet, but not so large that family members can photograph screen and identify others' medical status.

**05:00 PM** - End of day. Dr. Halloway prepares compliance certification memo for hospital leadership: triage system pilot approved pending anonymization fix, compliant with GDPR Article 5 (data minimization) and HIPAA Privacy Rule.

---

## Goals

### Primary Goals
1. **Eliminate privacy violations** - Ensure no patient names, medical details, or PHI appear on public displays or in unsecured logs
2. **Maintain compliance without sacrificing usability** - Privacy-compliant solutions must still be functional for patients and staff
3. **Reduce data liability** - Minimize data retention (24-hour patient data deletion) to reduce breach exposure
4. **Enable auditing while protecting patient privacy** - Comprehensive audit logs without exposing PHI

### Secondary Goals
- Define patient ID format that balances privacy, usability, and collision resolution
- Approve status message enums for public display (safe, non-medical terms)
- Review anonymization practices in application code and database
- Handle collision resolution for duplicate patient IDs
- Enforce GDPR data retention limits (30 days logs, 24-hour patient data)

---

## Pain Points (Linked to Registry)

| Pain Point ID | Description | Impact on Dr. Halloway |
|---------------|-------------|------------------------|
| PP-2.1 | Privacy violations with patient name displays | Current systems display full patient names on public boards, creating GDPR and HIPAA violations. This is non-negotiable compliance failure - system cannot go live with this design. |

---

## Frustrations

> "Every vendor pitches a system that displays full patient names on public boards. It's the first thing I have to strike down in every demo. GDPR and HIPAA are crystal clear: no PHI on public displays."

> "Data retention is a liability, not an asset. If you keep patient data for 6 months, you're creating a breach target. Minimize what you collect, delete what you don't need, and encrypt everything else."

> "Compliance isn't a checkbox at the end of development. It's a design constraint from day one. If the architecture doesn't support anonymization, you can't bolt it on later."

---

## Motivations

- **Patient Privacy First**: Dr. Halloway is deeply committed to protecting patient dignity and privacy. She's seen firsthand the emotional harm caused by privacy violations.
- **Legal Protection**: She knows that GDPR fines can reach 4% of annual revenue, and HIPAA violations can cost millions. Compliance protects the hospital from legal and financial disaster.
- **Ethical Responsibility**: Beyond legal requirements, Sarah believes healthcare organizations have a moral obligation to safeguard sensitive medical information.
- **Reputation Management**: Privacy breaches destroy public trust. Sarah protects the hospital's reputation by preventing violations before they occur.

---

## Technology Profile

| Aspect | Current | Desired |
|--------|---------|---------|
| Device | Desktop (policy review, audit logs) | Same, with automated compliance monitoring dashboard |
| Interface | Audit log viewers, policy documentation tools | Compliance dashboard showing real-time privacy metrics, audit trails |
| Training | Legal/policy background, technical literacy | Technical teams trained on privacy-by-design principles |
| Customization | Policy templates, approval workflows | Automated privacy impact assessments (DPIA) for new features |

### Technology Attitudes
- **Positive**: "I appreciate systems that build privacy in from the start - anonymization by default, minimal data collection, automatic deletion policies."
- **Skeptical**: "Most vendors treat compliance as an afterthought. They build the system, then ask us to approve it. That's backwards."
- **Pragmatic**: "Privacy and usability aren't opposites. A well-designed system can be both compliant and user-friendly. It just requires thinking about privacy constraints from day one."

---

## Scenarios

### Scenario 1: Privacy-Compliant Patient Identification
**Current Experience**: Vendor proposes displaying full patient names on public waiting room board (e.g., "John Smith - Waiting 30min"). Dr. Halloway rejects proposal, explains GDPR/HIPAA violations. Vendor must redesign from scratch, delaying project by 2 weeks.

**Desired Experience**: Vendor designs system with privacy-compliant patient IDs from day one (Initials + Day format: "JS-12"). Dr. Halloway reviews mockup, approves design with minor collision resolution clarification. No rework required, project stays on schedule.

### Scenario 2: Data Retention Policy Enforcement
**Current Experience**: Vendor stores patient data indefinitely (names, complaints, vitals) in database for "analytics and reporting." Dr. Halloway flags GDPR violation (data minimization principle), requires architecture change to implement 24-hour deletion policy. Major database redesign required.

**Desired Experience**: Vendor implements ephemeral data architecture from start: 24-hour automatic deletion for patient data, 30-day retention for anonymized audit logs. Dr. Halloway reviews data lifecycle documentation, approves design without changes.

### Scenario 3: Public Display Status Messages
**Current Experience**: Vendor proposes showing patient chief complaints on public display (e.g., "Chest Pain", "Abdominal Pain"). Dr. Halloway rejects as HIPAA violation (PHI disclosure). Vendor must redesign display with generic status messages.

**Desired Experience**: Vendor submits status message enum for approval: "Waiting for Triage", "Waiting for Doctor", "With Doctor", "Results Pending". No medical details. Dr. Halloway approves immediately, no redesign needed.

---

## Design Implications

### Privacy Requirements
- **Patient ID Format**: Initials + Day (e.g., "JS-12"), maximum 8 characters
- **No PHI on public displays**: No names, birthdates, complaints, vitals, or medical details visible
- **Status message enum**: Safe, non-medical terms only ("Waiting for Triage", "With Doctor")
- **Collision resolution protocol**: Append sequential number (JS-12-1, JS-12-2) for duplicate IDs
- **Anonymization by default**: No PHI in application logs, error messages, or database audit trails

### Data Retention Requirements
- **24-hour patient data deletion**: Names, complaints, vitals, ESI levels deleted automatically post-disposition
- **30-day audit log retention**: Anonymized audit logs kept for compliance, then purged
- **No long-term storage**: System must not accumulate patient data over time
- **Secure deletion**: Data must be cryptographically wiped, not just marked as deleted

### Audit Logging Requirements
- **Comprehensive audit trail**: All user actions logged (who accessed what, when, from where)
- **Anonymized logs**: Patient IDs (JS-12) used in logs, not real names
- **Tamper-proof logging**: Immutable audit trail for compliance investigations
- **Access monitoring**: Alerts for unusual data access patterns or privacy violations

---

## Quotes from Interviews

*From Session_1.2_The_Privacy___Compliance_Barrier.md:*

> "Dr. Halloway: We cannot display full patient names on public boards. GDPR and HIPAA are non-negotiable. Initials plus day format is the maximum we can show."

> "Question: What about displaying chief complaints? // Dr. Halloway: Absolutely not. 'Chest Pain' or 'Abdominal Pain' is protected health information. We use generic status messages like 'Waiting for Doctor' instead."

*From Session_2.1_Security___Operations_Finalization.md:*

> "Dr. Halloway: Data retention must follow GDPR minimization principles. Keep patient data for 24 hours post-disposition, then delete. Audit logs can stay for 30 days, but they must be anonymized."

> "Question: What happens if two patients have the same initials on the same day? // Dr. Halloway: Append a sequential number. 'JS-12-1' and 'JS-12-2'. Simple collision resolution."

---

## Traceability

| Link Type | IDs |
|-----------|-----|
| User Type | UT-2.2 |
| Pain Points | PP-2.1 |
| Client Facts | CF-C-001, CF-R-011, CF-C-002, CF-R-013, CF-R-014, CF-C-003, CF-R-016, CF-R-028, CF-R-029, CF-R-031 |
| Gaps | None |

---

**Document Status**: Complete
**Next**: Generate JTBD for this persona
