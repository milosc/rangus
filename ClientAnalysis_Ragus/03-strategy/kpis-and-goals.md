---
document_id: KPIS-Ragus
version: 1.0.0
created_at: 2026-02-17
updated_at: 2026-02-17
generated_by: Discovery_GenerateKPIs
source_files:
  - 03-strategy/product-vision.md
  - 03-strategy/product-strategy.md
  - 03-strategy/product-roadmap.md
  - 01-analysis/ANALYSIS_SUMMARY.md
change_history:
  - version: "1.0.0"
    date: "2026-02-17"
    author: "Discovery_GenerateKPIs"
    changes: "Initial KPI framework generation from strategy documents"
---

# KPIs and Goals: Ragus ER Triage System

**Created**: 2026-02-17
**Review Cycle**: Monthly
**Owner**: Product Manager

---

## 🎯 North Star Metric

### Intake-to-Triage Time

**Definition**: Elapsed time from patient arrival at intake desk to completion of triage assessment, measured in minutes.

**Formula**:
```
Intake-to-Triage Time = Triage_Complete_Timestamp - Intake_Complete_Timestamp
```

**Current Baseline**: 10+ minutes (as of 2026-02-17)
**12-Month Target**: <5 minutes (50% reduction)
**24-Month Target**: <3 minutes (70% reduction)

**Why This Metric**:
This metric directly reflects clinical safety and patient flow efficiency. Every minute of delay during triage increases mortality risk for urgent cases and creates waiting room bottlenecks. Reducing this time eliminates the fundamental trade-off between speed and safety that plague traditional ER systems. It encompasses intake speed, queue management, and clinical workflow velocity—the core value proposition of Ragus.

**Leading Indicators**:
- **Intake Time (Urgent Patients)**: <30 seconds predicts North Star will decrease (faster intake = faster triage)
- **Glove-Friendly Click Accuracy**: >95% accuracy predicts North Star will decrease (no workflow disruption from mis-clicks)
- **Float Staff Onboarding Time**: <30 seconds predicts sustained North Star (float staff can maintain velocity)

---

## 📊 KPI Framework

### Category 1: Efficiency Metrics

These metrics measure how well we're reducing waste and improving speed.

#### 1.1 Intake Time (Urgent Patients)

**Definition**: Time from patient arrival to "Intake Complete" status for urgent/trauma cases (P0 priority)
**Current**: 60-90 seconds
**Target**: <30 seconds
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: Application database (timestamp: `patient_created_at` → `intake_complete_at`)
- Collection: Automated
- Frequency: Real-time, aggregated hourly

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Emergency Bypass usage | 0% | >10% urgent cases | 20% |
| Keyboard vs mouse entry | 50% keyboard | >80% keyboard | 30% |
| Fields completed | 8 fields | 3 fields (Name, DOB, Complaint) | 50% |

---

#### 1.2 Triage Time per Patient

**Definition**: Time from nurse starting triage assessment to "Triaged" status (vitals captured, ESI assigned)
**Current**: 10+ minutes
**Target**: <5 minutes
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: Application database (timestamp: `triage_start_at` → `triaged_at`)
- Collection: Automated
- Frequency: Real-time, aggregated hourly

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Auto-advance queue usage | 0% | 100% | 40% |
| Glove-friendly click accuracy | <80% | >95% | 30% |
| Float staff vs regular staff time | Unknown | <60s vs 45s | 30% |

---

#### 1.3 Display Update Latency

**Definition**: Time delay between doctor assigning wait time slot and public display update, measured in seconds
**Current**: 1-2 seconds
**Target**: <1 second (sub-second latency)
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: WebSocket connection latency logs (server-side timestamp → client acknowledgement)
- Collection: Automated
- Frequency: Real-time monitoring, p95 latency reported hourly

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| WebSocket connection uptime | Unknown | >99.9% | 50% |
| Network round-trip time (LAN) | Unknown | <50ms | 30% |
| Patient confrontations due to lag | Multiple/shift | 0 | 20% |

---

### Category 2: Quality Metrics

These metrics measure accuracy, reliability, and satisfaction.

#### 2.1 GDPR/HIPAA Compliance Rate

**Definition**: Percentage of public display events that comply with privacy regulations (no full names, no medical details)
**Current**: Multiple violations detected (full names displayed)
**Target**: 100% compliance (0 violations)
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: Audit log system (30-day retention, anonymized patient IDs)
- Collection: Automated compliance scanner
- Frequency: Real-time scanning, daily reports

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Patient ID format (initials+day) | 0% | 100% | 40% |
| Medical details on public display | Yes | No | 30% |
| Full names on public display | Yes | No | 30% |

---

#### 2.2 System Uptime (LAN)

**Definition**: Percentage of time Ragus is operational on internal hospital LAN (excluding planned maintenance)
**Current**: Unknown (cloud-dependent system fails during internet outages)
**Target**: 99.9% uptime
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: Docker container health checks, VM monitoring
- Collection: Automated monitoring (Prometheus + Grafana)
- Frequency: Real-time, monthly uptime reports

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Internet outage resilience | 0% (system fails) | 100% (LAN-only operation) | 50% |
| VM snapshot recovery time | Unknown | <15 minutes | 30% |
| Zero data loss during outages | Not achieved | 100% | 20% |

---

#### 2.3 Clinical Control Rate

**Definition**: Percentage of patient time slot assignments made manually by doctor (vs. automated system escalation)
**Current**: <50% (automation overrides clinical judgment)
**Target**: 100% manual control
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: Application database (`time_slot_assigned_by` field)
- Collection: Automated
- Frequency: Real-time, aggregated per shift

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Automated escalation events | Multiple/shift | 0 | 60% |
| Doctor satisfaction (clinical control) | Unknown | >4/5 | 30% |
| Visual alert response time | N/A | <1 second | 10% |

---

### Category 3: Adoption Metrics

These metrics measure user engagement and growth.

#### 3.1 Float Staff Onboarding Time

**Definition**: Time from float staff first login to achieving <60-second triage time (productive without training)
**Current**: Requires buddy system (30-60 minutes)
**Target**: <30 seconds
**Timeline**: Phase 1 (Q1-Q2 2026)

**Measurement Method**:
- Data Source: Usability testing sessions, application database (first login → first triage completion time)
- Collection: Manual usability testing (n=10 float nurses), automated production tracking
- Frequency: Usability testing quarterly, production tracking real-time

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Float staff triage time | Unknown | <60s (vs 45s regular staff) | 50% |
| Float staff error rate | Unknown | <5% | 30% |
| Zero-training success rate | 0% | >90% | 20% |

---

#### 3.2 Daily Active Users (Clinical Staff)

**Definition**: Number of unique clinical staff users logging in daily
**Current**: Unknown (pilot deployment target: 15-20 staff)
**Target**: Phase 1: 15-20 users | Phase 2: 100-150 users | Phase 3: 1,000+ users
**Timeline**: Phase-dependent

**Measurement Method**:
- Data Source: LDAP authentication logs
- Collection: Automated
- Frequency: Daily active users (DAU) tracked real-time, weekly/monthly aggregates

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Clinical staff adoption rate | 0% | >90% within 2 weeks | 50% |
| Session duration per user | Unknown | >4 hours/shift | 30% |
| Feature usage rate (Kanban board) | 0% | >95% doctors | 20% |

---

#### 3.3 Hospital Deployment Growth

**Definition**: Number of emergency departments using Ragus in production
**Current**: 0 (pre-launch)
**Target**: Phase 1: 1 hospital | Phase 2: 5-10 hospitals | Phase 3: 50+ hospitals
**Timeline**: Phase-dependent

**Measurement Method**:
- Data Source: Sales/deployment tracker (CRM + manual records)
- Collection: Manual (weekly pipeline updates)
- Frequency: Monthly deployment reports

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Referral conversion rate | 0% | >80% (Phase 2) | 40% |
| Average contract size | Unknown | 1-10 ERs/contract | 30% |
| Time to deployment | Unknown | <15 minutes downtime | 30% |

---

### Category 4: Business Impact Metrics

These metrics measure financial and strategic outcomes.

#### 4.1 Patient Satisfaction (Wait Communication)

**Definition**: Patient-reported satisfaction rating (1-5 scale) for wait time communication and identification system
**Current**: Unknown (baseline to be established during pilot)
**Target**: >4/5 average rating
**Timeline**: Phase 1 (Q2 2026 baseline, ongoing)

**Measurement Method**:
- Data Source: Post-discharge patient surveys (optional, anonymized)
- Collection: Manual (tablet surveys at discharge desk)
- Frequency: Continuous collection, monthly aggregates

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Patient ID recognition | <50% | >95% | 40% |
| "Cattle" complaints | Multiple/month | 0 | 30% |
| Family tracking success rate | Unknown | >90% | 30% |

---

#### 4.2 Cost Savings (Time Reduction)

**Definition**: Annual cost savings from reduced staff time per patient (intake-to-triage time reduction)
**Current**: $0 (baseline)
**Target**: $150,000/year (single ER) | $1.5M/year (10 ERs)
**Timeline**: Phase 2 (Q3 2026 - Q1 2027)

**Measurement Method**:
- Data Source: Time savings calculation (minutes saved × patients/year × staff cost)
- Collection: Manual calculation from automated time metrics
- Frequency: Quarterly ROI reports

**Calculation**:
```
Annual Savings = (Baseline_Time - Current_Time) × Patients_Per_Year × Staff_Hourly_Cost

Example (Single ER):
(10 min - 5 min) × 20,000 patients/year × $45/hour ÷ 60 min/hour = $75,000/year
(Includes intake + triage nurse time savings)
```

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Staff time saved per patient | 0 min | 5 min | 60% |
| Annual patient volume | 20,000 | 20,000 | 20% |
| Staff utilization improvement | 0% | 20% | 20% |

---

#### 4.3 Annual Recurring Revenue (ARR)

**Definition**: Total annual contract value from all deployed hospitals
**Current**: $0 (pre-launch)
**Target**: Phase 1: $100K | Phase 2: $500K | Phase 3: $5M+
**Timeline**: Phase-dependent

**Measurement Method**:
- Data Source: Sales/finance records (contract values)
- Collection: Manual (monthly financial reports)
- Frequency: Monthly ARR tracking, quarterly business reviews

**Sub-Metrics**:
| Component | Current | Target | Weight |
|-----------|---------|--------|--------|
| Average contract value | Unknown | $50K-100K/ER/year | 50% |
| Customer retention rate | N/A | >95% | 30% |
| Upsell/expansion revenue | 0% | 20% of ARR | 20% |

---

## 🎯 Phase-Specific Goals

### Phase 1 Goals (Q1-Q2 2026)

| KPI | Current | Phase 1 Target | Measurement |
|-----|---------|----------------|-------------|
| Intake-to-Triage Time | 10+ min | <5 min | Database timestamps |
| Intake Time (Urgent Patients) | 60-90s | <30s | Database timestamps |
| Triage Time per Patient | 10+ min | <5 min | Database timestamps |
| Display Update Latency | 1-2s | <1s | WebSocket latency logs |
| GDPR/HIPAA Compliance Rate | Multiple violations | 100% | Audit logs |
| System Uptime (LAN) | Unknown | 99.9% | Container health checks |
| Clinical Control Rate | <50% | 100% | Database (manual vs automated) |
| Float Staff Onboarding Time | 30-60 min buddy system | <30s | Usability testing |
| Patient Satisfaction | Unknown | >4/5 | Post-discharge surveys |
| Hospital Deployments | 0 | 1 pilot ER | Sales tracker |

**Phase 1 Success Threshold**:
- Minimum: 70% of targets achieved (7/10 KPIs)
- Target: 90% of targets achieved (9/10 KPIs)

---

### Phase 2 Goals (Q3 2026 - Q1 2027)

| KPI | Phase 1 Target | Phase 2 Target | Measurement |
|-----|----------------|----------------|-------------|
| Intake-to-Triage Time | <5 min | <4 min | Database timestamps |
| System Uptime (LAN) | 99.9% | 99.95% | Container health checks |
| Deployment Time | 30+ min | <15 min | Deployment script logs |
| Eye Strain Rating (Night Shift) | >5/10 | <3/10 | Staff surveys |
| Hospital Deployments | 1 | 5-10 | Sales tracker |
| Daily Active Users | 15-20 | 100-150 | LDAP logs |
| Customer Satisfaction (NPS) | Unknown | >8/10 | NPS surveys |
| ARR | $100K | $500K | Financial records |
| Session Timeout Data Loss | Multiple/shift | 0 | Error logs |
| Cost Savings | $75K/ER/year | $750K/year (10 ERs) | ROI calculation |

**Phase 2 Success Threshold**:
- Minimum: 75% of targets achieved (8/10 KPIs)
- Target: 90% of targets achieved (9/10 KPIs)

---

### Phase 3 Goals (Q2 2027+)

| KPI | Phase 2 Target | Phase 3 Target | Measurement |
|-----|----------------|----------------|-------------|
| Intake-to-Triage Time | <4 min | <3 min | Database timestamps |
| Hospital Deployments | 10 | 50+ | Sales tracker |
| Daily Active Users | 150 | 1,000+ | LDAP logs |
| ARR | $500K | $5M+ | Financial records |
| Net Promoter Score | >8/10 | >50 | NPS surveys |
| Critical Bug Rate | Unknown | <1% | Bug tracking system |
| Response Time (p95) | Unknown | <500ms | Application performance monitoring |
| Cost Savings | $750K/year | $7.5M/year (100 ERs) | ROI calculation |

**Phase 3 Success Threshold**:
- Minimum: 80% of targets achieved (7/8 KPIs)
- Target: 95% of targets achieved (8/8 KPIs)

---

## 💰 ROI Calculation

### Investment Summary

#### Year 1 Costs (Phase 1)

| Category | Amount | Notes |
|----------|--------|-------|
| Development (Internal) | $680,000 | 8.5 FTE × $80K avg salary |
| Development (External) | $0 | No contractors in Phase 1 |
| Infrastructure | $20,000 | On-premise VM hardware, Docker licenses |
| Training | $5,000 | Clinical staff usability testing, training materials |
| Implementation | $10,000 | Pilot hospital deployment, onboarding |
| **Total Year 1** | **$715,000** | |

#### Ongoing Annual Costs (Post-Phase 1)

| Category | Amount | Notes |
|----------|--------|-------|
| Maintenance | $140,000 | 20% of development costs (internal team) |
| Infrastructure | $10,000 | Annual hosting/VM maintenance |
| Support | $50,000 | Clinical success lead + support engineer |
| **Total Annual** | **$200,000** | |

---

### Benefit Summary

#### Quantifiable Benefits (Annual - Single ER)

| Benefit | Calculation | Annual Value |
|---------|-------------|--------------|
| Time Savings (Clinical Staff) | 5 min/patient × 20,000 patients × $45/hour ÷ 60 min | $75,000 |
| Error Reduction (Privacy Violations) | 10 violations/year × $50K/violation | $500,000 |
| Productivity Gain (Float Staff) | 10% float staff × 20 staff × $90K salary | $18,000 |
| Tool Consolidation | N/A (no competing tools) | $0 |
| Revenue Impact (Compliance) | Zero GDPR/HIPAA fines | $500,000+ |
| **Total Annual Benefit (Single ER)** | | **$1,093,000** |

#### Quantifiable Benefits (Annual - 10 ERs, Phase 2)

| Benefit | Calculation | Annual Value |
|---------|-------------|--------------|
| Time Savings (Clinical Staff) | $75K × 10 ERs | $750,000 |
| Error Reduction (Privacy Violations) | $500K × 10 ERs | $5,000,000 |
| Productivity Gain (Float Staff) | $18K × 10 ERs | $180,000 |
| Revenue Impact (Compliance) | $500K × 10 ERs | $5,000,000 |
| **Total Annual Benefit (10 ERs)** | | **$10,930,000** |

#### Intangible Benefits
- **Patient Dignity Preservation**: Elimination of "cattle" complaints, improved patient experience (not easily quantifiable but significant reputational value)
- **Clinical Judgment Preservation**: 100% manual doctor control prevents inappropriate algorithmic prioritization (avoids potential patient harm lawsuits)
- **Staff Morale**: Reduction in eye strain (night shift dark mode), reduced confrontations with patients (sub-second display updates)
- **System Reliability**: Storm-proof operations (99.9% uptime) eliminates paper fallback chaos and productivity loss

---

### ROI Summary

| Metric | Value |
|--------|-------|
| **Total Investment (Year 1)** | $715,000 |
| **Annual Benefit (Single ER)** | $1,093,000 |
| **Net Annual Benefit (Single ER)** | $893,000 ($1,093,000 - $200,000 ongoing) |
| **Simple Payback Period** | 8 months |
| **3-Year ROI** | 273% [(3×$893K - $715K) ÷ $715K × 100] |
| **NPV (10% discount, 3 years)** | $1,507,000 |

**Phase 2 ROI (10 ERs)**:
| Metric | Value |
|--------|-------|
| **Additional Investment (Phase 2)** | $1,040,000 (13 FTE × $80K) |
| **Annual Benefit (10 ERs)** | $10,930,000 |
| **Net Annual Benefit (10 ERs)** | $10,730,000 ($10,930,000 - $200,000 ongoing) |
| **Cumulative 3-Year ROI** | 1,734% [(2×$10.73M + $893K - $715K - $1.04M) ÷ ($715K + $1.04M) × 100] |

**Break-Even Point**: Month 8 (Phase 1 pilot deployment)

---

## 📈 Measurement Plan

### Data Collection

| Metric | Source | Collection Method | Frequency | Owner |
|--------|--------|-------------------|-----------|-------|
| Intake-to-Triage Time | Application DB | Automated (timestamps) | Real-time | Backend Dev |
| GDPR/HIPAA Compliance | Audit logs | Automated scanner | Real-time | Compliance Officer |
| System Uptime | Container health checks | Automated monitoring (Prometheus) | Real-time | DevOps |
| Clinical Control Rate | Application DB | Automated (assigned_by field) | Real-time | Backend Dev |
| Float Staff Onboarding | Usability testing + DB | Manual testing + automated tracking | Quarterly / Real-time | UX Designer |
| Patient Satisfaction | Post-discharge surveys | Manual (tablet at discharge desk) | Continuous | Patient Rights Rep |
| Display Update Latency | WebSocket logs | Automated (server-client acknowledgement) | Real-time | Backend Dev |
| Hospital Deployments | Sales tracker | Manual (CRM + spreadsheet) | Weekly | Product Manager |
| ARR | Financial records | Manual (contract values) | Monthly | Finance |
| Cost Savings | ROI calculation | Manual (from time metrics) | Quarterly | Product Manager |

### Dashboard Requirements

| Dashboard | Audience | Metrics Included | Refresh Rate |
|-----------|----------|------------------|--------------|
| Executive | Leadership, Hospital Admin | North Star (Intake-to-Triage Time), ARR, ROI, Hospital Deployments | Weekly |
| Product | PM Team, UX Designer | All categories (Efficiency, Quality, Adoption, Business) | Daily |
| Operational | Clinical Staff, IT Ops | Efficiency metrics (Intake Time, Triage Time, Display Latency, System Uptime) | Real-time |
| Compliance | Compliance Officer, Legal | GDPR/HIPAA Compliance Rate, Audit Logs, Privacy Violations | Daily |

---

### Reporting Cadence

| Report | Frequency | Recipients | Focus |
|--------|-----------|------------|-------|
| Pulse Check | Weekly | Product team, engineers | Leading indicators (Intake Time, Display Latency, Float Staff Onboarding) |
| Progress Report | Bi-weekly | Stakeholders, pilot hospital | Phase goals, KPI tracking, blockers |
| Business Review | Monthly | Leadership, hospital admin | ROI, North Star, Hospital Deployments, ARR |
| Strategic Review | Quarterly | Executives, all stakeholders | Strategy alignment, Phase gate decisions, go-to-market adjustments |

---

## ⚠️ Metric Health Indicators

### Thresholds

| Metric | 🟢 On Track | 🟡 At Risk | 🔴 Off Track |
|--------|-------------|------------|--------------|
| Intake-to-Triage Time | <5 min | 5-7 min | >7 min |
| Intake Time (Urgent) | <30s | 30-45s | >45s |
| Triage Time | <5 min | 5-7 min | >7 min |
| Display Latency | <1s | 1-2s | >2s |
| GDPR/HIPAA Compliance | 100% | 99-99.9% | <99% |
| System Uptime | >99.9% | 99-99.9% | <99% |
| Clinical Control Rate | 100% | 95-99% | <95% |
| Float Staff Onboarding | <30s | 30-60s | >60s |
| Patient Satisfaction | >4/5 | 3.5-4/5 | <3.5/5 |
| Hospital Deployments | On pace (Phase-dependent) | 10% behind | >20% behind |

### Escalation Protocol

| Status | Action | Owner |
|--------|--------|-------|
| 🟢 On Track | Continue monitoring, celebrate wins | Product team |
| 🟡 At Risk | Root cause analysis, mitigation plan within 48 hours | Product Manager + Engineering Lead |
| 🔴 Off Track | Immediate review, course correction, leadership escalation | Leadership (VP Product, CTO) |

---

## 🎯 Baseline Establishment Plan

For metrics without current baselines:

| Metric | Data Needed | Collection Plan | Baseline By |
|--------|-------------|-----------------|-------------|
| Float Staff Triage Time | Usability testing with 10+ float nurses | Conduct usability study during Q1 2026 | Q2 2026 |
| Patient Satisfaction | Post-discharge surveys (n=50+) | Deploy tablet surveys at pilot hospital during Q2 2026 | Q3 2026 |
| Eye Strain Rating | Staff surveys (night shift staff, n=10+) | Conduct staff surveys during Q2 2026 | Q3 2026 |
| Response Time (p95) | Application performance monitoring | Deploy APM during Phase 2 | Q3 2026 |
| Critical Bug Rate | Bug tracking system (JIRA/Linear) | Begin tracking during Phase 1 | Q2 2026 |

---

**Document Status**: 🟢 Complete
**Created**: 2026-02-17
**Last Updated**: 2026-02-17
**Next Review**: 2026-03-17
