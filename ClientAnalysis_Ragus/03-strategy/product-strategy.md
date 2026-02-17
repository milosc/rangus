---
document_id: STRATEGY-Ragus
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GenerateStrategy
source_files:
  - 03-strategy/product-vision.md
  - 02-research/JOBS_TO_BE_DONE.md
  - 02-research/persona-intake-nurse.md
  - 02-research/persona-triage-nurse.md
  - 02-research/persona-triage-doctor.md
  - 02-research/persona-patient-advocate.md
  - 02-research/persona-it-compliance-lead.md
change_history:
  - version: "1.0.0"
    date: "2026-02-16"
    author: "Discovery_GenerateStrategy"
    changes: "Initial strategy document generation from vision and research"
---

# Product Strategy: Ragus

**Strategy Date**: 2026-02-16
**Planning Horizon**: 18 months (Q1 2026 - Q2 2027)
**Status**: 🟡 Draft

---

## 🎯 Strategic Objective

Transform emergency room triage from a dangerous, privacy-violating, anxiety-inducing bottleneck into a sub-30-second, GDPR/HIPAA-compliant, clinically-controlled workflow that operates reliably during internet outages while preserving patient dignity.

**North Star Metric**: Intake-to-Triage Time
**Target**: <5 minutes (50% reduction from 10+ minute baseline)

---

## 🏗️ Build vs. Buy Decision

**Decision**: BUILD

**Rationale**:
1. **No existing solution addresses the core trade-offs**: Commercial ER systems force impossible choices between speed vs. safety, privacy vs. recognition, automation vs. clinical judgment. Ragus eliminates these trade-offs through purpose-built clinical workflows designed by ER staff.
2. **On-premise LAN requirement eliminates SaaS options**: Internet outage resilience (99.9% uptime on internal LAN) is non-negotiable. Cloud-dependent systems fail during storms, forcing manual paper fallback—precisely the problem we're solving.
3. **Unique glove-friendly UX cannot be customized**: Float staff must learn the system in <30 seconds with zero training time. Commercial systems require extensive configuration and training, defeating the zero-training requirement.

**Risk Mitigation**: Modular architecture allows future integration with HL7/FHIR standards if hospital EMR interoperability becomes a requirement. Initial MVP focuses on standalone triage workflow without EMR dependencies.

---

## 🎯 Strategic Pillars

### Pillar 1: Clinical Workflow Velocity

**Goal**: Reduce intake-to-triage time from 10+ minutes to <5 minutes, with <30-second processing for urgent/trauma patients.

**Why This Pillar**:
Speed is the #1 clinical safety requirement. Every second delay during trauma arrivals increases mortality risk. Current systems force nurses to type frantically during life-threatening situations, creating dangerous delays and incomplete records. This pillar prioritizes workflow velocity through ultra-fast intake forms, keyboard shortcuts, glove-friendly touchscreens, and auto-advance queue features.

**Key Tactics**:
| # | Tactic | Owner | Timeline | Dependencies |
|---|--------|-------|----------|--------------|
| 1.1 | Design ultra-fast intake form (Name, DOB, Complaint only) with tab-enter navigation | UX Designer | Q1 2026 | None |
| 1.2 | Implement giant "Emergency Bypass" button for trauma cases (<10 sec processing) | Frontend Dev | Q1 2026 | 1.1 |
| 1.3 | Build auto-advance triage queue (next patient loads automatically) | Frontend Dev | Q1 2026 | None |
| 1.4 | Create glove-friendly UI (60x60px touch targets, one-click actions) | UX Designer | Q1 2026 | None |
| 1.5 | Optimize keyboard shortcuts for high-speed data entry | Frontend Dev | Q2 2026 | 1.1 |

**Success Metrics**:
- Intake Time (Urgent Patients): 60-90 seconds → <30 seconds
- Intake-to-Triage Wait Time: 10+ minutes → <5 minutes
- Triage Time per Patient: 10+ minutes → <5 minutes
- Glove-Friendly Click Accuracy: <80% → >95%

**Risks & Mitigations**:
| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Float staff unable to achieve <60s triage time | High | Medium | Intuitive UI with tooltips, logical workflow, discoverable actions |
| Emergency Bypass misused for non-urgent cases | Medium | Low | Audit logs, clinical workflow training, visual confirmation dialog |
| Tab-enter navigation conflicts with browser defaults | Medium | Medium | Custom keyboard event handlers, user testing with clinical staff |

---

### Pillar 2: Privacy-First Patient Experience

**Goal**: Achieve 100% GDPR/HIPAA compliance on public displays while maintaining patient dignity through recognizable identifiers (initials+day format).

**Why This Pillar**:
Current ER systems display full patient names on public waiting room screens, creating legal liability (GDPR/HIPAA violations) and patient complaints about privacy breaches. Alternative systems use dehumanizing numeric tickets ("734"), causing patients to forget their number and feel like "cattle." Ragus solves this with initials+day identifiers ("LC-16") that are privacy-compliant yet human-recognizable.

**Key Tactics**:
| # | Tactic | Owner | Timeline | Dependencies |
|---|--------|-------|----------|--------------|
| 2.1 | Generate privacy-compliant patient IDs (initials + day format: "LC-16") | Backend Dev | Q1 2026 | None |
| 2.2 | Design public display with category-based wait times (no countdown timers) | UX Designer | Q1 2026 | None |
| 2.3 | Implement 24-hour patient data deletion (GDPR compliance) | Backend Dev | Q2 2026 | None |
| 2.4 | Build audit log system (30-day retention, anonymized patient IDs) | Backend Dev | Q2 2026 | 2.1 |
| 2.5 | Create dark mode for public display (night shift, sensory overload reduction) | Frontend Dev | Q2 2026 | 2.2 |

**Success Metrics**:
- GDPR/HIPAA Violations: Multiple violations → 0 violations
- Patient Satisfaction (Wait Communication): Unknown → >4/5
- Patient Recognition of ID: <50% → >95%
- "Cattle" Complaints: Multiple/month → 0

**Risks & Mitigations**:
| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Patients forget their initials+day ID | Medium | Medium | Large, prominent ID display at intake; family members help track |
| Duplicate IDs (same initials on same day) | Low | High | Append collision counter ("LC-16-2"), test with high-volume scenarios |
| Audit log storage exceeds 30-day retention | Low | Low | Automated purge script, monitoring alerts |

---

### Pillar 3: Clinical Judgment Over Automation

**Goal**: Achieve 100% manual doctor control over patient prioritization with zero automated escalation based on wait time alone.

**Why This Pillar**:
Automated triage systems escalate patients based solely on wait time thresholds, ignoring critical visual clinical indicators like profuse sweating, agitation, or behavioral deterioration. Doctors report that algorithmic overrides force inappropriate prioritization and remove clinical judgment from medical decision-making. Ragus preserves manual control through time-based Kanban boards, visual wait-time alerts (yellow at 110%, red at 150%), and drag-and-drop patient management—without automated escalation.

**Key Tactics**:
| # | Tactic | Owner | Timeline | Dependencies |
|---|--------|-------|----------|--------------|
| 3.1 | Design Kanban board UI (To Be Triaged, 30m, 60m, 120m, Rest, With Doctor) | UX Designer | Q1 2026 | None |
| 3.2 | Implement drag-and-drop patient cards with one-click time slot buttons | Frontend Dev | Q1 2026 | 3.1 |
| 3.3 | Build visual wait-time alerts (yellow at 110%, red at 150%)—no auto-escalation | Frontend Dev | Q2 2026 | 3.1 |
| 3.4 | Create bulk update capability (multi-select patients, move to "With Doctor") | Frontend Dev | Q2 2026 | 3.2 |
| 3.5 | Implement behavioral risk flag (internal staff view only, not public) | Backend Dev | Q2 2026 | None |

**Success Metrics**:
- Manual Control: <50% → 100% manual time slot assignment
- Automated Escalation Events: Multiple/shift → 0 events
- Doctor Satisfaction (Clinical Control): Unknown → >4/5
- Visual Alert Response Time: N/A → <1 second

**Risks & Mitigations**:
| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Doctors ignore visual alerts (yellow/red borders) | High | Medium | Audio alerts (optional), clinical workflow training, alert fatigue monitoring |
| Drag-and-drop fails on gloves/touchscreens | Medium | Medium | Alternative one-click time slot buttons, user testing with gloves |
| Bulk update accidentally moves wrong patients | Medium | Low | Visual confirmation with patient count, undo capability |

---

### Pillar 4: Offline Reliability

**Goal**: Achieve 99.9% uptime on internal LAN with zero data loss during internet outages.

**Why This Pillar**:
Internet outages during storms cause complete system failure in cloud-dependent ER systems, forcing manual fallback to paper-based chaos. Patient queue data is lost, clinical staff revert to whiteboards, and productivity drops by 80%. Ragus operates on on-premise Ubuntu VMs with Docker deployment, zero cloud dependencies (no CDNs, no external APIs), and manual tarball updates—ensuring the system works during storms when it's needed most.

**Key Tactics**:
| # | Tactic | Owner | Timeline | Dependencies |
|---|--------|-------|----------|--------------|
| 4.1 | Design on-premise architecture (Ubuntu VM + Docker Compose) | Backend Architect | Q1 2026 | None |
| 4.2 | Bundle all assets in tarball (zero CDN dependencies) | DevOps | Q2 2026 | 4.1 |
| 4.3 | Implement manual deployment script (<15 min downtime) | DevOps | Q2 2026 | 4.2 |
| 4.4 | Build LAN-based real-time updates (WebSocket, sub-second latency) | Backend Dev | Q2 2026 | 4.1 |
| 4.5 | Create LDAP authentication integration (Active Directory) | Backend Dev | Q3 2026 | 4.1 |

**Success Metrics**:
- System Uptime (LAN): Unknown → 99.9%
- Internet Outage Data Loss: 100% → 0%
- Deployment Time: 30+ minutes → <15 minutes
- Display Update Latency: 1-2 seconds → <1 second

**Risks & Mitigations**:
| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Ubuntu VM failure (hardware/OS crash) | High | Low | VM snapshots, daily backups, hot standby VM |
| Docker container corruption during update | Medium | Low | Rollback script, container health checks, staging environment testing |
| LDAP/AD integration delays go-live | Medium | Medium | Phase 1 MVP uses basic auth; LDAP deferred to Phase 2 |

---

### Pillar 5: Zero-Training Usability

**Goal**: Float staff productive within 30 seconds, achieving <60-second triage time (vs. 45 seconds for regular staff).

**Why This Pillar**:
Float nurses arrive with zero system training due to vacation coverage, sick days, and shift changes. Current systems require buddy mentoring or 1-2 hour training sessions, creating workflow disruption and errors during high-volume periods. Ragus achieves zero-training onboarding through intuitive UI design, logical workflow layout, discoverable actions (tooltips, clear labels), and minimal cognitive load—ensuring float staff can triage effectively within 30 seconds of first login.

**Key Tactics**:
| # | Tactic | Owner | Timeline | Dependencies |
|---|--------|-------|----------|--------------|
| 5.1 | Design intuitive UI with logical workflow (intake → triage → doctor review) | UX Designer | Q1 2026 | None |
| 5.2 | Implement discoverable actions (tooltips, inline help, contextual hints) | Frontend Dev | Q2 2026 | 5.1 |
| 5.3 | Minimize cognitive load (clear labels, color-coded buttons, visual hierarchy) | UX Designer | Q1 2026 | 5.1 |
| 5.4 | Conduct usability testing with float staff (target: <60s triage time) | UX Researcher | Q2 2026 | 5.1, 5.2 |
| 5.5 | Implement dark mode for night shifts (auto-toggle at 19:00-07:00) | Frontend Dev | Q2 2026 | None |

**Success Metrics**:
- Float Staff Onboarding Time: Requires buddy system → <30 seconds
- Float Staff Triage Time: Unknown → <60 seconds (vs. 45s for regular staff)
- Float Staff Error Rate: Unknown → <5%
- Eye Strain Rating (Night Shift): >5/10 → <3/10

**Risks & Mitigations**:
| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| UI too simple for power users (regular staff) | Low | Medium | Keyboard shortcuts for advanced users, customizable preferences |
| Tooltips ignored during high-stress situations | Medium | Medium | Visual design hierarchy, progressive disclosure, contextual positioning |
| Dark mode reduces readability for some users | Low | Medium | Manual toggle override, high-contrast mode, user preference settings |

---

## 📊 Pillar Interdependencies

```
[Clinical Velocity] ──enables──▶ [Zero-Training Usability]
        │                                │
        │                                │
        ▼                                ▼
[Privacy-First UX] ◀──requires── [Offline Reliability]
                                         ▲
                                         │
                            [Clinical Judgment] ──depends on──
```

### Dependency Matrix

| Pillar | Depends On | Enables |
|--------|------------|---------|
| Clinical Velocity | None (foundational) | Zero-Training Usability |
| Privacy-First UX | Offline Reliability (on-premise data storage) | Clinical Judgment (trust in system) |
| Clinical Judgment | Offline Reliability (real-time updates) | None |
| Offline Reliability | None (foundational) | Privacy-First UX, Clinical Judgment |
| Zero-Training Usability | Clinical Velocity (fast workflow) | None |

---

## 🎭 Go-To-Market Strategy

### Phase 1: Single-ER Pilot (Q1-Q2 2026, 6 months)

**Objective**: Validate core workflows with one emergency department, achieve <5-minute intake-to-triage time, and prove reliability during internet outages.

**Target Segment**:
- **Users**: 15-20 clinical staff (intake nurses, triage nurses, triage doctor, patient advocate, IT lead)
- **Size**: 1 emergency room (medium-volume: 40-60 patients/shift)
- **Characteristics**: Early adopter hospital willing to provide detailed feedback, receptive to iterative improvements, located in storm-prone region (validates offline reliability)

**Value Proposition**:
Pilot hospital gains 50% reduction in intake-to-triage wait time, achieves GDPR/HIPAA compliance, and eliminates manual paper fallback during internet outages—in exchange for detailed clinical workflow feedback and co-design participation.

**Channels**:
| Channel | Purpose | Metrics |
|---------|---------|---------|
| Direct relationship (existing client) | Hospital stakeholder buy-in, co-design workshops | Weekly feedback sessions, NPS >8/10 |
| On-site shadowing | Observe clinical workflows in real ER environment | 5+ shadowing sessions, workflow documentation |
| Iterative demos | Validate UI/UX with clinical staff before development | 3+ demo cycles, >90% feature approval |

**Success Criteria**:
- [x] Intake-to-triage time <5 minutes (baseline: 10+ minutes)
- [x] <30-second processing for urgent patients (baseline: 60-90 seconds)
- [x] 100% manual doctor control (zero automated escalation events)
- [x] Zero GDPR/HIPAA violations on public display
- [x] System uptime >99% on internal LAN during pilot
- [x] Float staff productive within 60 seconds (zero training time)
- [x] Patient satisfaction >4/5 for wait time communication

---

### Phase 2: Multi-Site Expansion (Q3 2026 - Q1 2027, 6 months)

**Objective**: Deploy to 5-10 emergency departments across multiple hospital systems, validate scalability, and refine deployment process.

**Target Segment**:
- **Users**: 100-150 clinical staff across 5-10 emergency departments
- **Size**: Medium to large ERs (40-100 patients/shift)
- **Characteristics**: Hospitals experiencing GDPR/HIPAA compliance issues, dissatisfaction with current ER systems, storm-prone regions requiring offline reliability

**Value Proposition**:
Proven clinical workflow velocity (50% reduction in wait times), zero-training float staff onboarding, and guaranteed system uptime during internet outages—with streamlined deployment process (<15 minutes downtime per hospital).

**Channels**:
| Channel | Purpose | Metrics |
|---------|---------|---------|
| Hospital network referrals | Pilot hospital advocates to peer institutions | 5+ referrals, >80% conversion |
| Case studies | Demonstrate quantified clinical outcomes (wait time reduction, compliance) | 3+ case studies, public presentations |
| Regional health conferences | Showcase live demo, clinical staff testimonials | 2+ conference presentations, 50+ qualified leads |

**Success Criteria**:
- [x] 5-10 hospitals deployed successfully
- [x] Deployment time <15 minutes per hospital
- [x] Zero critical bugs during multi-site rollout
- [x] System uptime >99.5% across all sites
- [x] Customer satisfaction >8/10 NPS
- [x] Clinical staff adoption >90% within 2 weeks

---

### Phase 3: National Rollout (Q2 2027+, ongoing)

**Objective**: Scale to 50+ emergency departments nationally, establish Ragus as the ER triage standard for privacy-first, offline-reliable clinical workflows.

**Target Segment**:
- **Users**: 1,000+ clinical staff across 50+ emergency departments
- **Size**: All ER types (small rural clinics to large urban trauma centers)
- **Characteristics**: Any hospital prioritizing clinical safety, patient privacy, and system reliability over cloud convenience

**Value Proposition**:
Industry-standard ER triage system with proven clinical outcomes, regulatory compliance, and offline reliability—backed by multi-site case studies and clinical staff endorsements.

**Channels**:
| Channel | Purpose | Metrics |
|---------|---------|---------|
| Direct sales team | Target large hospital systems (10+ ERs per contract) | 10+ hospital systems, $5M+ ARR |
| Channel partners | Regional healthcare IT vendors (deployment and support) | 5+ partners, 30% indirect revenue |
| Industry publications | Peer-reviewed clinical outcomes (JAMA Emergency Medicine) | 1+ publication, 100+ citations |

**Success Criteria**:
- [x] 50+ hospitals deployed
- [x] 1,000+ clinical staff using system daily
- [x] $5M+ annual recurring revenue
- [x] <1% critical bug rate
- [x] Net Promoter Score >50
- [x] Industry recognition (awards, publications)

---

## 💰 Resource Strategy

### Team Requirements

| Role | Phase 1 | Phase 2 | Phase 3 |
|------|---------|---------|---------|
| Product Manager | 1.0 FTE | 1.0 FTE | 1.5 FTE |
| UX Designer | 1.0 FTE | 1.0 FTE | 2.0 FTE |
| Frontend Developer | 2.0 FTE | 3.0 FTE | 5.0 FTE |
| Backend Developer | 2.0 FTE | 3.0 FTE | 5.0 FTE |
| QA Engineer | 1.0 FTE | 2.0 FTE | 3.0 FTE |
| DevOps Engineer | 1.0 FTE | 2.0 FTE | 3.0 FTE |
| Clinical Success Lead | 0.5 FTE | 1.0 FTE | 2.0 FTE |
| **Total** | **8.5 FTE** | **13.0 FTE** | **21.5 FTE** |

### Investment Areas

| Area | Phase 1 | Phase 2 | Phase 3 | Total |
|------|---------|---------|---------|-------|
| Development | 60% | 55% | 50% | 55% |
| Design/UX | 15% | 10% | 10% | 12% |
| Clinical Success | 10% | 15% | 20% | 15% |
| DevOps/Infrastructure | 10% | 15% | 15% | 13% |
| Sales/Marketing | 5% | 5% | 5% | 5% |

---

## 🎯 Competitive Strategy

### Positioning

**Primary Differentiator**: Clinical workflows designed BY ER staff, FOR ER staff—prioritizing speed, privacy, and clinical judgment over algorithmic automation.

**Secondary Differentiators**:
- Offline reliability (99.9% uptime on internal LAN during internet outages)
- Zero-training float staff onboarding (<30 seconds to productivity)
- Privacy-first patient IDs (initials+day format: GDPR/HIPAA compliant yet human-recognizable)
- 100% manual doctor control (zero automated escalation)

### Competitive Response Matrix

| Competitor Move | Our Response |
|-----------------|--------------|
| Cloud-based competitor adds offline mode | Highlight their retrofit approach vs. our native on-premise architecture; emphasize data residency and tarball deployment simplicity |
| Competitor adds privacy-compliant patient IDs | Emphasize full workflow integration (not just public display) and clinical staff co-design validation |
| Competitor adds manual control toggle | Highlight their default-automated approach vs. our manual-by-design philosophy; clinical judgment baked into every decision |
| Competitor undercuts pricing | Emphasize TCO (no cloud fees, no per-user licensing, no vendor VPN delays); focus on clinical outcomes ROI |

---

## ⚠️ Strategic Risks

### Risk Register

| # | Risk | Impact | Likelihood | Mitigation | Owner |
|---|------|--------|------------|------------|-------|
| R1 | Pilot hospital feedback reveals fundamental workflow misalignment | High | Medium | Weekly shadowing sessions, iterative demo cycles, co-design workshops with clinical staff | Product Manager |
| R2 | Float staff cannot achieve <60s triage time (zero-training fails) | High | Medium | Extensive usability testing, tooltips/inline help, progressive disclosure design | UX Designer |
| R3 | On-premise deployment exceeds 15-minute downtime window | Medium | Medium | Automated deployment scripts, rollback procedures, staging environment validation | DevOps Engineer |
| R4 | LDAP/AD integration delays Phase 1 go-live | Medium | Medium | Phase 1 MVP uses basic auth; LDAP deferred to Phase 2 | Backend Architect |
| R5 | Patient ID collisions (duplicate initials+day) cause confusion | Medium | High | Append collision counter ("LC-16-2"), test with high-volume scenarios | Backend Developer |
| R6 | WebSocket real-time updates fail on hospital network (firewall/proxy) | High | Low | Fallback to polling (5-second intervals), hospital IT network assessment pre-deployment | Backend Developer |

### Assumptions to Validate

| Assumption | Validation Method | Timeline | Decision if Wrong |
|------------|-------------------|----------|-------------------|
| Float staff can learn system in <30 seconds | Usability testing with 10+ float nurses | Q2 2026 | Extend onboarding time, add training materials, simplify UI further |
| Glove-friendly UI achieves >95% click accuracy | User testing with gloves on touchscreens | Q1 2026 | Increase touch target sizes, adjust button spacing, test on multiple devices |
| Category-based wait times reduce patient anxiety | Patient surveys, confrontation incident tracking | Q2 2026 | Add additional messaging, consider optional countdown timers (controlled rollout) |
| On-premise deployment meets hospital IT security requirements | Security audits, compliance checklists | Q1 2026 | Add additional security controls, pursue SOC 2 certification if needed |
| Kanban drag-and-drop works with gloves/touchscreens | User testing with triage doctors | Q2 2026 | Provide alternative one-click time slot buttons as fallback |

---

## 📈 Strategy Review Cadence

| Review Type | Frequency | Participants | Focus |
|-------------|-----------|--------------|-------|
| Tactical | Weekly | Product team, engineers | Sprint progress, blockers, pilot hospital feedback |
| Strategic | Monthly | Leadership, product team | Pillar progress, KPI tracking, risk mitigation |
| Vision | Quarterly | All stakeholders, pilot hospital | Direction alignment, Phase gate decisions, go-to-market adjustments |

---

**Document Status**: 🟡 Draft
**Created**: 2026-02-16
**Next Review**: 2026-03-16
**Owner**: Product Team
