---
persona_id: P-2.1
version: 1.0.0
created_at: 2026-02-16
updated_at: 2026-02-16
generated_by: Discovery_GeneratePersona
source_user_type: UT-2.1
---

# Persona: Marcus "The Fortress" Thompson

**Archetype**: IT Manager / Operations
**Persona ID**: P-2.1
**Based on User Type**: UT-2.1 (IT Manager / Operations)

---

## Profile Summary

| Attribute | Value |
|-----------|-------|
| Name | Marcus Thompson |
| Nickname | "The Fortress" |
| Age | 38 |
| Experience | 15 years in healthcare IT, 6 years managing hospital infrastructure |
| Shift | On-call 24/7, primary hours 8 AM - 6 PM |
| Primary Tool | SSH terminals, Docker Compose, VM management console |
| Tech Comfort | Very High - Expert in infrastructure, security, and Linux administration |

---

## Background

Marcus has spent 15 years in healthcare IT, with the last 6 years managing the hospital's on-premise infrastructure. He's earned the nickname "The Fortress" because of his unwavering commitment to system reliability and security. Marcus believes in defense-in-depth: redundant systems, hourly snapshots, air-gapped networks, and zero external dependencies.

He's seen cloud systems fail during critical moments - internet outages during storms, vendor services going down at 3 AM with no local fallback. Marcus refuses to let his ER depend on external connectivity. His mantra is simple: "If the internet goes down, the internal LAN stays up, and so does the triage system."

Marcus manages on-premise VM infrastructure running Ubuntu 22.04 (4 vCPUs, 16GB RAM), handles network VLAN configuration, firewall rules, SSL/TLS certificates (self-signed for pilot), and LDAP/Active Directory integration. He performs manual deployments via Docker Compose, delivered as tarballs since vendor VPN access requires a 2-week security approval process. He's also responsible for enforcing the hospital's 15-minute idle timeout policy for security compliance.

---

## A Day in Marcus' Life

**08:00 AM** - Marcus arrives at the office, checks monitoring dashboard for overnight VM health. All systems green - hourly snapshots completed successfully, no failed services.

**09:30 AM** - Security team requests SSL certificate renewal for triage system. Marcus generates new self-signed cert (pilot doesn't have budget for commercial CA), updates Docker Compose config, plans manual deployment for low-traffic window (2 PM).

**10:45 AM** - Vendor emails tarball update for triage system (bug fix). Marcus can't grant vendor VPN access (2-week approval process), so he downloads tarball, verifies checksums, extracts to staging directory.

**12:00 PM** - Tests update in staging environment (separate VM). Runs smoke tests: login flow, patient creation, display updates. All functional.

**02:00 PM** - Maintenance window. Marcus stops Docker containers, applies update, restarts services. Triage system back online in 8 minutes. Validates real-time display updates working correctly (sub-second latency via WebSocket).

**03:30 PM** - Configuring LDAP integration for new clinical staff user. Tests authentication against Active Directory, grants RBAC permissions (Clinical role, not View-Only).

**05:15 PM** - Storm warning issued. Marcus verifies backup power systems (UPS) are charged. Internet connectivity may be lost, but internal LAN and on-premise triage system will remain operational.

**07:45 PM** (Evening, on-call)** - Storm hits, internet connection lost. Marcus receives alert, but triage system continues operating normally on internal LAN. Clinical staff experience zero disruption. External cloud systems (EHR) are offline, but standalone triage pilot unaffected.

**09:00 PM** - Internet restored. Marcus verifies all services are healthy, reviews logs for any anomalies during outage. Triage system operated flawlessly in air-gapped mode.

---

## Goals

### Primary Goals
1. **Ensure system remains operational during internet outages** - On-premise deployment with zero external dependencies
2. **Maintain security compliance** - SSL/TLS encryption, LDAP authentication, 15-minute idle timeout, hourly snapshots
3. **Minimize vendor dependencies** - Manual tarball deployments, no VPN access required for routine updates
4. **Enable simple, reliable deployments** - Docker Compose for consistency, repeatable update process

### Secondary Goals
- Configure network VLANs and firewall rules for triage system isolation
- Manage LDAP/Active Directory integration for single sign-on
- Enforce 15-minute idle timeout policy for security compliance
- Maintain hourly VM snapshots for disaster recovery
- Approve and monitor vendor access (when absolutely necessary)

---

## Pain Points (Linked to Registry)

| Pain Point ID | Description | Impact on Marcus |
|---------------|-------------|------------------|
| PP-3.1 | Internet dependency creates system failure risk | Cloud-based systems fail during storms or outages, but internal LAN remains operational. Marcus cannot risk losing patient queue data due to connectivity issues. |
| PP-6.1 | Vendor access requires 2-week approval | External vendor VPN access requires lengthy security review, preventing rapid bug fixes and updates. Must use manual tarball/patch delivery instead. |
| PP-6.2 | Session timeout causes data loss | Strict 15-minute idle timeout for security compliance can cause loss of partially completed forms, creating frustration for clinical staff. |

---

## Frustrations

> "Cloud systems are great until the internet goes down. During storm season, we can't afford to lose the triage system just because Comcast has an outage. Everything has to work on the internal LAN."

> "Vendor VPN access takes 2 weeks to approve. That's unacceptable when we need a critical bug fix deployed. I'd rather handle tarballs and manual deployments than wait for security paperwork."

> "The 15-minute idle timeout is a security requirement, but clinical staff complain about losing form data. We need better session management that doesn't compromise security."

---

## Motivations

- **System Reliability**: Marcus takes personal pride in maintaining 99.9% uptime. His infrastructure has survived storms, power outages, and network failures without impacting clinical operations.
- **Security First**: He knows that healthcare data is a prime target for cyberattacks. Every decision is filtered through a security lens - encryption, authentication, network isolation, audit logging.
- **Operational Independence**: Marcus values systems that don't depend on external vendors or internet connectivity. Self-sufficiency means faster responses to issues and fewer points of failure.
- **Simplicity in Deployment**: He prefers simple, repeatable deployment processes (Docker Compose) over complex orchestration systems that require specialized knowledge.

---

## Technology Profile

| Aspect | Current | Desired |
|--------|---------|---------|
| Device | SSH terminal, VM management console | Same, with improved deployment automation |
| Interface | Command-line (Docker Compose, systemctl) | CLI preferred, with optional monitoring dashboard |
| Training | Self-taught, 15 years experience | Comprehensive deployment docs, runbooks for updates |
| Customization | Full control over VM config, network, certificates | Same level of control, streamlined deployment process |

### Technology Attitudes
- **Positive**: "I trust on-premise infrastructure I can see and control. Docker Compose is simple, reliable, and doesn't require a PhD to understand."
- **Skeptical**: "Cloud vendors promise 99.99% uptime, but I've seen them go down during critical moments. I'd rather own the infrastructure."
- **Pragmatic**: "If it works without the internet, survives power outages, and can be updated with a tarball, it's good enough for me."

---

## Scenarios

### Scenario 1: Internet Outage During Storm
**Current Experience**: Hospital internet connection lost during storm. Cloud-based EHR system offline. Clinical staff can't access patient records. Triage workflow disrupted.

**Desired Experience**: Internet connection lost during storm. Triage system (on-premise) continues operating on internal LAN. Clinical staff experience zero disruption - intake, triage, doctor dashboard, public display all functional. Patient queue data preserved.

### Scenario 2: Vendor Bug Fix Deployment
**Current Experience**: Vendor identifies critical bug, offers to deploy fix. Marcus must initiate 2-week VPN access approval process. Bug remains unfixed for 2+ weeks while paperwork processes.

**Desired Experience**: Vendor emails tarball with bug fix, release notes, and checksum. Marcus downloads tarball, verifies integrity, tests in staging VM, deploys to production during maintenance window. **Total time: 3 hours from notification to production deployment.**

### Scenario 3: SSL Certificate Renewal
**Current Experience**: Self-signed SSL certificate expires. Marcus generates new cert manually, updates Docker Compose YAML, stops containers, applies config, restarts. Process requires 15 minutes of downtime during low-traffic window.

**Desired Experience**: Self-signed SSL certificate with 1-year validity. Deployment script automates cert rotation: generates cert, updates config, performs rolling restart with zero downtime. Marcus reviews and approves automated renewal.

---

## Design Implications

### Infrastructure Requirements
- **On-premise deployment mandatory** - No cloud dependencies, no external API calls
- **Air-gapped operation** - Bundle all assets (fonts, libraries, images) in Docker image, no CDN dependencies
- **Docker Compose architecture** - Simple, single-file orchestration for VM deployment
- **Ubuntu 22.04 compatibility** - Target OS for hospital VM infrastructure (4 vCPUs, 16GB RAM)
- **Internal LAN only** - System must function without internet access

### Security Requirements
- **SSL/TLS encryption mandatory** - Even on internal LAN (hospital policy)
- **Self-signed certificates acceptable for pilot** - Budget constraints, future migration to commercial CA
- **LDAP/Active Directory integration** - Single sign-on via hospital authentication system
- **RBAC (Role-Based Access Control)** - Clinical role vs. View-Only role vs. Admin role
- **15-minute idle timeout enforcement** - Security compliance requirement
- **Audit logging** - All user actions logged for compliance

### Deployment Requirements
- **Tarball delivery** - Vendor VPN access not available during pilot
- **Manual deployment via Docker Compose** - Simple, repeatable process
- **Hourly VM snapshot compatibility** - System state must be snapshot-friendly (no in-flight transactions breaking on restore)
- **Network VLAN isolation** - Triage system on isolated VLAN segment with firewall rules

---

## Quotes from Interviews

*From Session_1.3_Infrastructure_and_Interoperability.md:*

> "Marcus: We can't rely on internet connectivity. During storm season, we lose external connections regularly. Everything has to work on the internal LAN."

> "Question: What's your process for vendor updates? // Marcus: Vendor sends us a tarball. We test it in staging, then deploy manually. VPN access takes 2 weeks to approve, so we don't bother."

*From Session_2.1_Security___Operations_Finalization.md:*

> "Marcus: Self-signed SSL certificates are fine for the pilot. We'll migrate to a commercial CA if the system goes into production."

> "Question: What's your disaster recovery process? // Marcus: Hourly VM snapshots. If something breaks, we restore from the most recent snapshot. Never lost more than an hour of data."

---

## Traceability

| Link Type | IDs |
|-----------|-----|
| User Type | UT-2.1 |
| Pain Points | PP-3.1, PP-6.1, PP-6.2 |
| Client Facts | CF-C-004, CF-C-005, CF-O-003, CF-O-004, CF-R-018, CF-O-005, CF-C-006, CF-O-006, CF-C-007, CF-O-007, CF-C-008, CF-R-027, CF-R-030, CF-R-032, CF-R-033, CF-C-009 |
| Gaps | None |

---

**Document Status**: Complete
**Next**: Generate JTBD for this persona
