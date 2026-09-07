# SECURITY+ MISSION ATLAS — PLANNING ARCHIVE

*Continuous working record: Atlas Register → Mission 01 Passport (pressure-test reconciliation) → Architecture Governance. Preserved as a full history rather than a trimmed end-state, so future contributors — human or AI — can trace how each design decision was reached. Author contact details redacted.*

---

# PART 1 — MISSION ATLAS REGISTER

# SECURITY+ MISSION ATLAS

# MISSION ATLAS REGISTER

**VERSION:** 1.0 — Master Architecture
**STATUS:** Architecture Baseline / Mission Passports in Development
**DESTINATION:** CompTIA Security+ V7
**PRIMARY MISSION SET:** 01–09

---

# 01 — ATLAS PURPOSE

The Mission Atlas is the master architecture for a systems-journey learning program whose destination is **CompTIA Security+ V7**.

The Atlas is not a textbook.

It is not a collection of nine unrelated projects.

It is not a duplicate of the Mission Passports.

The Atlas exists to answer:

> **How do the missions collectively produce complete Security+ coverage while building progressively deeper systems understanding?**

The learner studies Security+ through interesting real-world systems.

Each mission provides a different system journey.

Security concepts recur naturally across those journeys.

The learner therefore encounters the same concepts in different environments rather than studying them once and forgetting them.

---

## Governing Principle

> **Security+ is the destination. The Mission Atlas is the vehicle.**

---

## Passport / Atlas Boundary

### The Mission Passport owns:

- mission intent
- scenario
- system architecture
- detailed questions
- concepts to discover
- labs
- failure scenarios
- attack scenarios
- tangible deliverables
- evidence requirements
- mission-specific open questions
- curiosity branches
- deferred topics
- mission handoff instructions
- detailed execution state

### The Atlas Register owns:

- mission architecture
- mission sequencing
- mission purpose
- Security+ atomic coverage
- mission ownership
- cross-mission reinforcement
- intended coverage depth
- verification gaps
- cross-mission dependencies
- final aggregate coverage

**Rule:**

> If the information already belongs authoritatively in a Mission Passport, the Atlas does not reproduce it.

---

# 02 — MISSION REGISTER

The Atlas currently consists of nine primary system journeys.

The missions are intentionally different.

They do **not** need to represent one fictional organization or one continuously evolving system.

The learner should repeatedly encounter familiar security concepts in unfamiliar environments.

---

## MISSION 01 — HOW DOES MY PHONE REACH GOOGLE?

**Primary purpose:**

Networking, communications, cryptography, architecture, identity, and end-to-end systems reasoning.

**System journey:**

> Human → Phone → Cellular Network → Carrier → Internet → Google

**Primary Security+ territory:**

- networking
- secure communications
- cryptography
- PKI
- authentication
- authorization
- wireless security
- infrastructure
- attack surfaces
- monitoring
- evidence

**Role in Atlas:**

Foundational systems vocabulary.

---

## MISSION 02 — HOW DOES STARLINK GET A PACKET TO THE INTERNET?

**Primary purpose:**

Wireless communications, satellite networking, routing, distributed infrastructure, resilience, and physical infrastructure.

**System journey:**

> User → Ground/terminal system → Satellite constellation → Ground infrastructure → Internet

**Primary Security+ territory:**

- wireless
- resilience
- availability
- routing
- distributed infrastructure
- physical security
- communications security
- infrastructure diversity
- failure recovery

**Role in Atlas:**

Expands networking concepts into a radically different physical and distributed environment.

---

## MISSION 03 — BUILD THE SECURE INNOVATION LAB

**Primary purpose:**

Build a functioning enterprise-like environment and secure it deliberately.

**System journey:**

> Requirements → Architecture → Systems → Identity → Network → Security Controls → Monitoring

**Primary Security+ territory:**

- security controls
- segmentation
- access control
- secure baselines
- hardening
- firewalls
- IDS/IPS
- DNS filtering
- NAC
- IAM
- monitoring
- automation
- change management

**Role in Atlas:**

Primary enterprise security architecture and control implementation mission.

---

## MISSION 04 — THE NETWORK IS COMPROMISED

**Primary purpose:**

Investigate a security incident rather than merely learning about attacks.

**System journey:**

> Normal System → Suspicious Activity → Detection → Investigation → Containment → Root Cause → Recovery

**Primary Security+ territory:**

- threat actors
- attack surfaces
- vulnerabilities
- malicious activity
- mitigation
- monitoring
- incident response
- threat hunting
- digital forensics
- data sources
- root cause analysis

**Role in Atlas:**

Primary threat, vulnerability, detection, and incident-response mission.

---

## MISSION 05 — BUILD A SECURE AI CAPABILITY

**Primary purpose:**

Understand and secure a modern AI-enabled application/capability.

**System journey:**

> User → Application → API → AI Service → Data → Infrastructure → Response

**Primary Security+ territory:**

- application security
- cloud security
- data protection
- APIs
- identity
- access control
- cryptography
- vulnerabilities
- secure configuration
- automation
- privacy
- supply chain

**Role in Atlas:**

Primary modern application/data/AI security mission.

---

## MISSION 06 — BUILD THE DRONE ISR SYSTEM

**Primary purpose:**

Secure a mobile, wireless, operationally important system.

**System journey:**

> Sensor → Drone → Wireless Link → Network → Operations Center → Analyst

**Primary Security+ territory:**

- wireless security
- mobile solutions
- authentication
- secure communications
- availability
- resilience
- physical security
- endpoint security
- monitoring
- attack surfaces

**Role in Atlas:**

Applies previously learned security concepts to a physical/mobile operational system.

---

## MISSION 07 — MOVE THE SYSTEM TO THE CLOUD

**Primary purpose:**

Transform an existing capability into a cloud architecture.

**System journey:**

> Existing System → Cloud Architecture → Identity → Network → Data → Services → Monitoring → Recovery

**Primary Security+ territory:**

- cloud architecture
- IAM
- secure access
- data protection
- resilience
- backups
- availability
- automation
- infrastructure security
- vulnerability management

**Role in Atlas:**

Primary cloud architecture and cloud security mission.

---

## MISSION 08 — THE SYSTEM NOBODY UNDERSTANDS

**Primary purpose:**

Move from technical security into governance, risk, compliance, and third-party management.

**System journey:**

> Technology → Organization → Risk → Policy → Vendors → Compliance → Oversight

**Primary Security+ territory:**

- governance
- policies
- standards
- procedures
- roles
- risk
- risk register
- risk appetite/tolerance
- BIA
- third-party risk
- compliance
- audits
- assessments
- awareness

**Role in Atlas:**

Primary Security Program Management and Oversight mission.

---

## MISSION 09 — EVERYTHING IS FAILING

**Primary purpose:**

Integrate security, resilience, continuity, recovery, and systems thinking under simultaneous failure.

**System journey:**

> Normal Operations → Multiple Failures → Detection → Response → Continuity → Recovery → Lessons Learned

**Primary Security+ territory:**

- resilience
- high availability
- redundancy
- recovery
- continuity
- backups
- power
- site considerations
- platform diversity
- incident response
- risk
- architecture
- capstone integration

**Role in Atlas:**

Final systems-resilience and integration mission.

---

# 03 — ATLAS OPERATING MODEL

The missions are not a textbook sequence.

A later mission may reuse concepts from an earlier mission, but the earlier mission does not automatically become a prerequisite.

The Atlas deliberately uses:

> **Different systems + recurring concepts + increasing complexity**

rather than:

> **One fictional system becoming progressively larger.**

---

## Mission Progression

The broad learning progression is:

```
01  Understand a real system
        ↓
02  Compare a radically different system
        ↓
03  Build and secure a system
        ↓
04  Investigate a compromised system
        ↓
05  Secure a modern application capability
        ↓
06  Secure a mobile/physical operational system
        ↓
07  Transform the architecture into the cloud
        ↓
08  Govern the resulting system
        ↓
09  Keep systems operating when everything fails
```

This is a **learning progression**, not a rigid prerequisite chain.

---

# 04 — COVERAGE MODEL

Every Security+ atomic requirement belongs in the Atlas.

No requirement may disappear because it does not naturally fit one mission.

However:

> **Every requirement does not need to be owned by every mission.**

---

## Planned Coverage Vocabulary

The coverage shown in this Register represents the **intended state at mission completion**.

It is **not actual learner progress**.

### 🟢 Demonstrated

The owning mission is expected to produce practical evidence.

Examples:

- configuration
- implementation
- controlled failure
- investigation
- analysis
- remediation
- validation
- applied architecture

### 🟡 Understood

The mission is expected to produce meaningful explanation/application evidence, but practical implementation is not its primary purpose.

### 🔵 Encountered

The concept naturally appears in the mission and is retained in the learner's conceptual model, but deeper ownership belongs elsewhere.

### ⚪ Not a Mission Target

The concept is intentionally not owned by that mission.

This is not a failure.

It means the Atlas is preventing artificial mission bloat.

### 🟣 Exam Verified

Reserved for **actual later exam verification**.

It is not a planned mission-completion status.

---

# 05 — SECURITY+ ATOMIC COVERAGE MAP

This is the **master crossover and ownership map**.

It simultaneously records:

- the atomic requirement
- primary mission ownership
- reinforcing missions
- intended depth
- whether a Verification Lab may be required

The Mission Passports remain authoritative for the actual treatment.

---

# DOMAIN 1 — GENERAL SECURITY CONCEPTS

## 1.1 — Security Controls

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|1.1-A|Compare technical controls|M03|M01, M04, M07|🟢|
|1.1-B|Compare preventive controls|M03|M04, M09|🟢|
|1.1-C|Compare managerial controls|M08|M03|🟢|
|1.1-D|Compare deterrent controls|M03|M08|🟡|
|1.1-E|Compare operational controls|M03|M04, M08|🟢|
|1.1-F|Compare detective controls|M04|M03, M09|🟢|
|1.1-G|Compare physical controls|M06|M02, M09|🟡|
|1.1-H|Compare corrective controls|M04|M09|🟢|
|1.1-I|Compare compensating controls|M08|M03, M09|🟡|
|1.1-J|Compare directive controls|M08|M03|🟢|

---

## 1.2 — Fundamental Security Concepts

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|1.2-A|Confidentiality|M01|M03, M05, M06, M07|🟢|
|1.2-B|Integrity|M01|M04, M05, M06|🟢|
|1.2-C|Availability|M09|M02, M06, M07|🟢|
|1.2-D|Non-repudiation|M01|M05, M08|🟡|
|1.2-E|Authentication|M01|M03, M06, M07|🟢|
|1.2-F|Authorization|M03|M05, M07|🟢|
|1.2-G|Accounting|M03|M04, M08|🟡|
|1.2-H|Zero Trust|M03|M05, M07|🟢|
|1.2-I|Deception/disruption technology|M04|M03|🟡|

---

## 1.3 — Change Management

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|1.3-A|Business processes associated with change management|M03|M08|🟡|
|1.3-B|Technical implications of changes|M03|M07, M09|🟢|
|1.3-C|Change documentation|M03|M08|🟢|
|1.3-D|Version control|M05|M03, M07|🟢|

---

## 1.4 — Cryptographic Solutions

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|1.4-A|PKI|M01|M03, M05, M06, M07|🟢|
|1.4-B|Encryption|M01|M03, M05, M06, M07|🟢|
|1.4-C|Obfuscation|M05|M04, M07|🟡|
|1.4-D|Hashing|M01|M04, M05|🟢|
|1.4-E|Digital signatures|M01|M05, M06, M07|🟢|
|1.4-F|Blockchain|—|M05|🔵|

**1.4-F note:** Blockchain is deliberately not forced into the core mission architecture. It remains an encountered/verification topic unless later evidence justifies deeper treatment.

---

# DOMAIN 2 — THREATS, VULNERABILITIES & MITIGATIONS

## 2.1 — Threat Actors and Motivations

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|2.1-A|Nation-state threat actors|M04|M06, M08|🟡|
|2.1-B|Unskilled attackers|M04|M03|🟡|
|2.1-C|Hacktivists|M04|M08|🟡|
|2.1-D|Insider threats|M04|M08|🟢|
|2.1-E|Organized crime|M04|M05, M08|🟡|
|2.1-F|Shadow IT|M08|M05, M07|🟢|
|2.1-G|Data exfiltration motivation|M04|M05, M08|🟢|
|2.1-H|Espionage motivation|M04|M06, M08|🟡|
|2.1-I|Financial gain motivation|M04|M05, M08|🟡|

---

## 2.2 — Threat Vectors and Attack Surfaces

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|2.2-A|Message-based vectors|M04|M05, M08|🟡|
|2.2-B|Unsecure network vectors|M04|M01, M02, M06|🟢|
|2.2-C|Social engineering vectors|M04|M08|🟡|
|2.2-D|File-based vectors|M04|M05|🟡|
|2.2-E|Voice call vectors|M04|M06|🔵|
|2.2-F|Supply chain vectors|M05|M04, M08|🟡|
|2.2-G|Vulnerable software vectors|M04|M05, M07|🟢|
|2.2-H|Attack surfaces|M04|M01, M03, M05, M06, M07|🟢|

---

## 2.3 — Vulnerabilities

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|2.3-A|Application vulnerabilities|M05|M04, M07|🟢|
|2.3-B|Hardware vulnerabilities|M06|M02, M04|🟡|
|2.3-C|Mobile device vulnerabilities|M06|M01, M04|🟢|
|2.3-D|Virtualization vulnerabilities|M07|M03, M05|🟡|
|2.3-E|OS-based vulnerabilities|M04|M03, M05, M07|🟢|
|2.3-F|Cloud-specific vulnerabilities|M07|M05|🟢|
|2.3-G|Web-based vulnerabilities|M05|M04|🟢|
|2.3-H|Supply chain vulnerabilities|M05|M08|🟡|

---

## 2.4 — Malicious Activity

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|2.4-A|Malware attacks|M04|M05, M07|🟢|
|2.4-B|Password attacks|M04|M03, M07|🟢|
|2.4-C|Application attacks|M05|M04|🟢|
|2.4-D|Physical attacks|M06|M02, M04|🟡|
|2.4-E|Network attacks|M04|M01, M02, M03, M06|🟢|
|2.4-F|Cryptographic attacks|M04|M01, M05|🟡|

---

## 2.5 — Mitigation Techniques

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|2.5-A|Segmentation|M03|M04, M05, M07, M09|🟢|
|2.5-B|Access control|M03|M04, M05, M06, M07|🟢|
|2.5-C|Configuration enforcement|M03|M05, M07|🟢|
|2.5-D|Hardening|M03|M04, M05, M07|🟢|
|2.5-E|Isolation|M03|M04, M06, M09|🟢|
|2.5-F|Patching|M04|M03, M05, M07|🟢|

---

# DOMAIN 3 — SECURITY ARCHITECTURE

## 3.1 — Architecture Models

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|3.1-A|On-premises architecture|M03|M07|🟢|
|3.1-B|Cloud architecture|M07|M05, M03|🟢|
|3.1-C|Virtualization architecture|M07|M03, M05|🟡|
|3.1-D|IoT architecture|M06|M05|🟡|
|3.1-E|ICS architecture|—|M03, M08|🔵|
|3.1-F|Infrastructure as Code|M07|M03, M05|🟢|

---

## 3.2 — Enterprise Infrastructure

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|3.2-A|Infrastructure considerations|M03|M01, M02, M06, M07|🟢|
|3.2-B|Control selection|M03|M04, M07, M08|🟢|
|3.2-C|Secure communication|M01|M02, M05, M06, M07|🟢|
|3.2-D|Secure access|M03|M01, M05, M06, M07|🟢|

---

## 3.3 — Data Protection

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|3.3-A|Relevant data types|M05|M07, M08|🟢|
|3.3-B|Data securing methods|M05|M01, M03, M07|🟢|
|3.3-C|Data protection considerations|M05|M07, M08|🟢|
|3.3-D|Data classifications|M08|M05, M07|🟢|

---

## 3.4 — Resilience and Recovery

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|3.4-A|High availability|M09|M02, M06, M07|🟢|
|3.4-B|Site considerations|M09|M02, M07|🟡|
|3.4-C|Resilience/recovery testing|M09|M04, M07|🟢|
|3.4-D|Power considerations|M09|M02, M06|🟡|
|3.4-E|Platform diversity|M09|M02, M07|🟢|
|3.4-F|Backups|M09|M05, M07|🟢|
|3.4-G|Continuity of operations|M09|M08|🟢|

---

# DOMAIN 4 — SECURITY OPERATIONS

## 4.1 — Computing Resources

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.1-A|Secure baselines|M03|M04, M05, M07|🟢|
|4.1-B|Mobile solutions|M06|M01|🟢|
|4.1-C|Hardening|M03|M04, M05, M06, M07|🟢|
|4.1-D|Wireless security|M06|M01, M02|🟢|
|4.1-E|Application security|M05|M03, M04, M07|🟢|
|4.1-F|Sandboxing|M05|M03, M07|🟡|
|4.1-G|Monitoring computing resources|M04|M03, M05, M06, M07|🟢|

---

## 4.2 — Asset Management

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.2-A|Hardware/software/data acquisition|M08|M03, M07|🟡|
|4.2-B|Asset disposal|M08|M03|🟡|
|4.2-C|Asset assignment|M08|M03, M07|🟡|
|4.2-D|Asset monitoring/tracking|M08|M03, M04, M06|🟢|

Mission 08 owns the lifecycle perspective; the technical missions encounter assets in context.

---

## 4.3 — Vulnerability Management

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.3-A|Identify vulnerabilities|M04|M03, M05, M07|🟢|
|4.3-B|Analyze vulnerabilities|M04|M05, M07|🟢|
|4.3-C|Remediate vulnerabilities|M04|M03, M05, M07|🟢|
|4.3-D|Validate remediation|M04|M03, M07|🟢|
|4.3-E|Report vulnerabilities|M04|M08|🟢|

**Required lifecycle:**

> Identify → Analyze → Remediate → Validate → Report

A scanner alone does not satisfy this objective.

---

## 4.4 — Alerting and Monitoring

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.4-A|Monitoring tools|M04|M03, M05, M06, M07|🟢|
|4.4-B|Computing resource activities relevant to monitoring|M04|M03, M05, M07|🟢|

---

## 4.5 — Enterprise Security

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.5-A|Firewalls|M03|M04, M07, M09|🟢|
|4.5-B|IDS/IPS|M03|M04|🟢|
|4.5-C|DNS filtering|M03|M04, M05|🟢|
|4.5-D|DLP|M03|M05, M07, M08|🟡|
|4.5-E|NAC|M03|M07|🟡|
|4.5-F|EDR/XDR|M04|M03, M05, M07|🟢|

---

## 4.6 — Identity and Access Management

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.6-A|Provisioning|M07|M03, M08|🟢|
|4.6-B|SSO|M07|M03, M05|🟢|
|4.6-C|MFA|M07|M03, M05|🟢|
|4.6-D|Privileged access tools|M07|M03, M08|🟢|

---

## 4.7 — Automation and Orchestration

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.7-A|Automation use cases|M07|M03, M05|🟢|
|4.7-B|Scripting benefits|M03|M04, M05, M07|🟢|
|4.7-C|Automation considerations|M07|M03, M05|🟢|

---

## 4.8 — Incident Response

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.8-A|Incident response processes|M04|M09|🟢|
|4.8-B|Incident response training|M04|M08|🟡|
|4.8-C|Incident response testing|M04|M09|🟢|
|4.8-D|Root cause analysis|M04|M09|🟢|
|4.8-E|Threat hunting|M04|M05, M07|🟢|
|4.8-F|Digital forensics|M04|M01, M05|🟢|

Security+ SY0-701 treats incident response as objective 4.8 and data sources separately as 4.9. ([O'Reilly Media](https://www.oreilly.com/library/view/comptia-security-sy0-701/9780138293215/ch22.xhtml))

---

## 4.9 — Data Sources

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|4.9-A|Use log data to support investigations|M04|M03, M05, M07|🟢|
|4.9-B|Use other data sources to support investigations|M04|M01, M03, M05, M07|🟢|

Relevant investigation sources include firewall, application, endpoint, OS, IDS/IPS, network logs, metadata, vulnerability scans, automated reports, dashboards, and packet captures. ([Packt Publishing](https://www.packtpub.com/en-sg/product/comptia-security-sy0-701-certification-guide-third-edition-9781835461532/chapter/chapter-22-given-a-scenario-use-data-sources-to-support-an-investigation-26/section/exam-objectives-49-ch26lvl1sec58))

---

# DOMAIN 5 — SECURITY PROGRAM MANAGEMENT & OVERSIGHT

## 5.1 — Security Governance

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|5.1-A|Guidelines|M08|M03|🟢|
|5.1-B|Policies|M08|M03, M07|🟢|
|5.1-C|Standards|M08|M03, M07|🟢|
|5.1-D|Procedures|M08|M03, M04|🟢|
|5.1-E|External considerations|M08|M07|🟢|
|5.1-F|Monitoring within governance|M08|M04|🟢|
|5.1-G|Governance structures|M08|—|🟢|
|5.1-H|Roles/responsibilities|M08|M03|🟢|

---

## 5.2 — Risk Management

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|5.2-A|Risk identification|M08|M03, M04, M07, M09|🟢|
|5.2-B|Risk assessment|M08|M03, M04, M07|🟢|
|5.2-C|Risk analysis|M08|M04, M07, M09|🟢|
|5.2-D|Risk register|M08|M03, M09|🟢|
|5.2-E|Risk tolerance|M08|M09|🟢|
|5.2-F|Risk appetite|M08|M09|🟢|
|5.2-G|Risk strategies|M08|M03, M07, M09|🟢|
|5.2-H|Risk reporting|M08|M09|🟢|
|5.2-I|BIA|M08|M09|🟢|

---

## 5.3 — Third-Party Risk

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|5.3-A|Vendor assessment|M08|M05, M07|🟢|
|5.3-B|Vendor selection|M08|M05, M07|🟢|
|5.3-C|Vendor agreements|M08|M05, M07|🟢|
|5.3-D|Vendor monitoring|M08|M07|🟢|
|5.3-E|Vendor questionnaires|M08|—|🟢|
|5.3-F|Rules of engagement|M08|M04|🟢|

---

## 5.4 — Security Compliance

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|5.4-A|Compliance reporting|M08|M03, M07|🟢|
|5.4-B|Consequences of non-compliance|M08|—|🟢|
|5.4-C|Compliance monitoring|M08|M03, M07|🟢|
|5.4-D|Privacy considerations|M08|M05, M07|🟢|

---

## 5.5 — Audits and Assessments

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|5.5-A|Attestation|M08|—|🟡|
|5.5-B|Internal audits|M08|M03, M04|🟢|
|5.5-C|External audits|M08|—|🟡|
|5.5-D|Penetration testing|M04|M03, M05, M07|🟢|

---

## 5.6 — Security Awareness

|ID|Atomic requirement|Primary|Reinforcement|Target|
|---|---|---|---|---|
|5.6-A|Phishing training|M08|M04|🟡|
|5.6-B|Recognize anomalous behavior|M04|M08|🟢|
|5.6-C|User guidance|M08|M03, M04|🟢|
|5.6-D|User reporting|M08|M04|🟢|
|5.6-E|Monitoring|M08|M04|🟢|

---

# 06 — CROSS-MISSION RELATIONSHIPS

This section exists only to identify **meaningful learning crossover**.

It does not duplicate the Security+ Coverage Map.

---

## Networking

**M01 → M02 → M03 → M04 → M06 → M07 → M09**

The learner repeatedly encounters networking under different physical, architectural, and security constraints.

---

## Wireless

**M01 → M02 → M06**

The same fundamental communication concepts are encountered through:

- cellular
- satellite
- drone/operational wireless

This creates comparison rather than repetition.

---

## Cryptography

**M01 → M03 → M05 → M06 → M07**

Cryptography progresses from:

> "How does this connection become trusted?"

to:

> "How do I deliberately architect cryptographic protection into a system?"

---

## Identity

**M01 → M03 → M06 → M07**

Identity progresses from real-world communication identity into enterprise IAM and cloud access.

---

## Attack Surface

**M01 → M03 → M04 → M05 → M06 → M07**

The learner first learns to see attack surfaces, then builds them, then investigates their exploitation.

---

## Vulnerabilities

**M03 → M04 → M05 → M06 → M07**

The learner moves from configuration weaknesses to active investigation and then into application, mobile, and cloud environments.

---

## Monitoring and Evidence

**M01 → M03 → M04 → M05 → M07 → M09**

Evidence becomes increasingly important as the learner moves from:

> "What happened?"

to:

> "How can I prove what happened?"

to:

> "How do I detect and investigate it operationally?"

---

## Resilience

**M01 → M02 → M06 → M07 → M09**

Resilience is progressively reinterpreted through:

- network paths
- satellite infrastructure
- mobile operations
- cloud architecture
- total-system failure

---

## Data Protection

**M01 → M05 → M07 → M08**

Data moves from:

> protection in transit

to:

> application/data security

to:

> cloud data architecture

to:

> governance, classification, privacy, and compliance.

---

## Risk

**M03 → M04 → M05 → M07 → M08 → M09**

Risk eventually becomes an explicit management discipline rather than merely a technical security consideration.

---

## Incident Response

**M03 → M04 → M07 → M09**

The learner first builds controls, then sees what happens when controls fail, then applies response concepts to cloud systems, and finally handles systemic failure.

---

# 07 — VERIFICATION LAB REGISTER

Verification Labs exist to close requirements that the missions cannot naturally demonstrate at sufficient depth.

They should **not** be created merely because a Security+ requirement exists.

The first candidate gaps are:

|Area|Likely treatment|
|---|---|
|1.4-F Blockchain|Encountered / targeted verification if required|
|3.1-E ICS architecture|Encountered / targeted verification if required|
|5.5-A Attestation|Understood through M08; verification if needed|
|5.5-C External audits|Understood through M08; verification if needed|
|5.6-A Phishing training|Understood through M08; verification if needed|
|Specialized Security+ terminology|Targeted exam verification|
|Any requirement remaining 🟡 after mission completion|Targeted verification|
|Any requirement remaining 🔵 after mission completion|Dedicated learning/verification activity|

### Verification rule

A Verification Lab is created **after** the missions have been designed and executed enough to determine that a genuine gap remains.

It is not pre-created merely to inflate coverage.

---

# 10 — MISSION EXECUTION GOVERNANCE

The Atlas does not dictate how each mission is executed.

Each Mission Passport does that.

The Atlas governs only the relationship between missions.

---

## Mission Lifecycle

```
PLANNED
   ↓
DESIGNED
   ↓
ACTIVE
   ↓
EVIDENCE PRODUCED
   ↓
MISSION COMPLETE
   ↓
SECURITY+ COVERAGE UPDATED
   ↓
CROSSOVER REVIEW
   ↓
GAPS TRANSFERRED
   ↓
ATLAS UPDATED
```

---

## Coverage Integrity Rule

The Atlas must never claim:

> "The learner knows this because Mission 03 mentioned it."

Instead:

> "Mission 03 was designed to provide this level of coverage."

Actual learner evidence remains inside the mission execution record.

---

## Ownership Rule

Every important Security+ requirement should have a primary home whenever practical.

A mission may reinforce another mission's concept without becoming its owner.

This prevents the same material from being rebuilt repeatedly.

---

## No Artificial Mission Inflation

A mission should not add an activity solely because a Security+ requirement is difficult to place.

If the requirement does not naturally belong:

1. record it;
2. assign it to another mission;
3. or use a Verification Lab.

---

# 11 — FINAL ATLAS COVERAGE

The final Atlas question is not:

> "Did every mission teach everything?"

It is:

> **"Does the complete Atlas, in aggregation, account for every Security+ atomic requirement at an appropriate depth?"**

---

## Atlas Completeness

At final design:

```
Every atomic Security+ requirement
        ↓
Has a primary home OR deliberate verification path
        ↓
May have reinforcing missions
        ↓
Points to the relevant Mission Passport
        ↓
Can eventually produce evidence
```

Therefore the Atlas is considered **coverage-complete** when:

- every atomic requirement appears in the Coverage Map;
- every requirement has a deliberate treatment decision;
- every requirement is either owned by a mission, encountered intentionally, or assigned to verification;
- no requirement is silently omitted;
- no requirement is falsely claimed as demonstrated;
- cross-mission reinforcement is visible;
- the actual passports contain the detailed treatment.

---

## Final Learner Coverage

Only after missions are executed can the learner's real status be determined:

|Status|Meaning|
|---|---|
|⚪|Not encountered|
|🔵|Encountered|
|🟡|Understood|
|🟢|Demonstrated|
|🟣|Exam verified|

The Atlas design therefore separates:

**Planned coverage**

from

**Actual evidence**

from

**Exam verification**.

That distinction is permanent.

---

# 12 — HANDOFF / CONTINUITY PROTOCOL

The Mission Atlas is designed so that another AI can continue the project without reconstructing its philosophy.

A new AI should understand:

## Destination

CompTIA Security+ V7.

## Method

Learn through real systems journeys rather than arbitrary textbook sequencing.

## Master Architecture

Mission Atlas + Mission Passports.

## Authority

The Mission Passport is authoritative for mission-specific execution.

The Atlas Register is authoritative for cross-mission architecture and Security+ coverage.

## Current Missions

01 — Phone → Google
02 — Starlink → Internet
03 — Secure Innovation Lab
04 — Network Compromised
05 — Secure AI Capability
06 — Drone ISR System
07 — Move the System to the Cloud
08 — System Nobody Understands
09 — Everything Is Failing

## Security+ Mapping

The atomic requirement IDs in the Coverage Map are authoritative.

The Atlas must use:

`1.1-A` through `5.6-E`

rather than inventing alternate objective numbering.

## Coverage Philosophy

A requirement appearing in a mission does not automatically mean it is demonstrated.

Coverage must distinguish:

- Demonstrated
- Understood
- Encountered
- Not a Mission Target

Actual learner status later uses:

- ⚪
- 🔵
- 🟡
- 🟢
- 🟣

## Mission Philosophy

Do not force every mission to become a miniature Security+ course.

Do not force every Security+ requirement into every mission.

Do not make all journeys variations of the same fictional enterprise.

Use different interesting systems.

Allow concepts to recur naturally.

Allow concepts to deepen through different contexts.

Use Verification Labs when necessary.

---

# ATLAS MASTER RULE

> **The Mission Passports contain the missions.**
>
> **The Atlas Register contains the architecture connecting them.**
>
> **The Security+ Coverage Map contains the master ownership and crossover model.**
>
> **The complete Atlas is successful when every atomic Security+ requirement has a deliberate home somewhere in the combined system.**

---

# CURRENT ATLAS STATE

**Mission 01:** Passport architecture complete.

**Mission 02:** Mission concept established; Passport not yet built.

**Mission 03:** Mission concept established; Passport not yet built.

**Mission 04:** Mission concept established; Passport not yet built.

**Mission 05:** Mission concept established; Passport not yet built.

**Mission 06:** Mission concept established; Passport not yet built.

**Mission 07:** Mission concept established; Passport not yet built.

**Mission 08:** Mission concept established; Passport not yet built.

**Mission 09:** Mission concept established; Passport not yet built.

**Security+ atomic matrix:** Established.

**Mission crossover model:** Established.

**Mission ownership model:** Incorporated into Security+ Coverage Map.

**Verification model:** Established.

**Tangible deliverable register:** Intentionally left to Mission Passports.

**Curiosity/deferred register:** Intentionally left to Mission Passports.

**Final aggregate coverage:** Defined; actual learner status remains pending mission execution.

---

# FINAL DESIGN DECISION

The Atlas is intentionally **not** a second copy of the passports.

It is the **control layer above them**.

The intended relationship is:

```
                         SECURITY+ V7
                              │
                              ▼
                    ┌───────────────────┐
                    │   ATLAS REGISTER  │
                    │                   │
                    │ Mission Map       │
                    │ Coverage Map      │
                    │ Relationships     │
                    │ Verification      │
                    │ Final Aggregation │
                    └─────────┬─────────┘
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
        MISSION 01       MISSION 02       MISSION 03
        PASSPORT         PASSPORT         PASSPORT
             │                │                │
             └────────────────┼────────────────┘
                              │
                           ...09
                              │
                              ▼
                     ACTUAL EVIDENCE
                              │
                              ▼
                    SECURITY+ VERIFICATION
```

The **Mission Atlas Register is therefore complete as the master planning architecture**. The next work is not to expand this register with mission-level details. It is to use this register to construct **Mission 02's Passport**, then 03, and so on, checking each new passport against this master map.

---

# PART 2 — DESIGN DECISION RECORD

*The following preserves the planning correspondence in which the Mission 01 Passport was reconciled against the pressure test. Retained verbatim (with author contact redacted) because it records the frozen architectural decisions in the author's own words.*

> **Working label at the time:** Master Passport 1
>
> Yes. The pressure test you pasted is the authoritative version. I'm treating that as the frozen architectural decision and rebuilding the passport around it.
>
> The important corrections are:
>
> - **No separate parent-objective coverage column.**
> - Coverage is now recorded **at the atomic Security+ requirement level**.
> - The color/status represents **expected coverage by Mission 01 completion**, not the learner's current state.
> - Every atomic requirement is accounted for.
> - **Demonstrated / Understood / Encountered / Not a Mission 01 Target** are planning classifications, not evidence that has already been earned.
> - **4.8 Incident Response** and **4.9 Data Sources** are separated.
> - The passport remains a handoff document: another AI should be able to pick it up without reconstructing the design decisions.

---

# Security+ Mission Atlas — Mission 01

# SECURITY+ MISSION ATLAS

## MISSION PASSPORT

**MISSION:** 01 — How Does My Phone Reach Google?
**VERSION:** 2.0 — Final Architecture Baseline
**STATUS:** Designed / Not Executed
**DESTINATION:** CompTIA Security+ V7

---

# 1. DESTINATION

**CompTIA Security+ V7**

The mission is a vehicle for demonstrating Security+ knowledge.

It is not a substitute for the Security+ requirements.

The Security+ requirements are maintained independently in the Atlas Sub-Element Requirements Matrix.

Mission 01 is responsible for accounting for every atomic requirement and identifying what level of coverage the mission is expected to provide.

---

# 2. MISSION INTENT

Understand the complete end-to-end journey of information from a mobile device to an Internet service and back.

The mission begins with a deceptively simple question:

> **What actually happens when I type `google.com` into my phone while driving past a cell tower?**

The objective is not merely to learn cellular networking.

The objective is to develop the ability to:

- trace information through a complex system
- identify the components involved
- understand how devices communicate
- understand how identities are established
- understand how information is protected
- understand how information is addressed and routed
- identify trust boundaries
- identify attack surfaces
- identify security controls
- analyze failures
- investigate evidence
- understand dependencies
- modify a system safely
- deliberately break portions of a system
- determine why they failed
- apply mitigations
- explain the entire system coherently
- map demonstrated knowledge to Security+

Security+ concepts will be introduced when they become necessary to answer questions about the system.

---

# 3. SCENARIO

You are using a smartphone while traveling down a highway.

You open a browser and enter:

`https://www.google.com/`

You press Enter.

Within moments, Google responds.

The mission is to reconstruct what happened.

We want to understand the journey from:

**Human → Application → Phone → Radio → Cellular Network → Carrier Core → Internet → Google → Response**

at progressively deeper levels.

---

# 4. END STATE

Mission 01 is complete when the learner can independently:

1. Draw the major architecture involved in the journey.
2. Trace the request from application to destination and the response back.
3. Explain the major roles of the cellular radio network, transport network, carrier core, Internet, and destination infrastructure.
4. Explain addressing and name resolution at the relevant levels.
5. Explain the major protocols involved.
6. Explain where authentication and authorization occur.
7. Explain how confidentiality and integrity are established.
8. Explain the role of certificates and PKI.
9. Identify meaningful trust boundaries and attack surfaces.
10. Identify relevant security controls.
11. Analyze selected failure scenarios.
12. Investigate actual network evidence where practical.
13. Build a simplified representation of the system.
14. Deliberately break portions of the simplified system.
15. Explain the resulting behavior.
16. Apply appropriate mitigations.
17. Investigate evidence following a simulated security event.
18. Perform root-cause analysis on selected failures.
19. Map the demonstrated knowledge back to Security+ atomic requirements.
20. Identify which Security+ requirements remain outside the mission's ownership.
21. Produce tangible evidence of learning.
22. Deliver a coherent **"Phone → Google" systems narrative** without relying on a prepared script.

---

# 5. WHY THIS MISSION EXISTS

This is the foundational systems mission of the Atlas.

A single web request crosses multiple technological domains:

- mobile computing
- wireless communications
- networking
- switching
- routing
- addressing
- DNS
- transport protocols
- application protocols
- encryption
- authentication
- PKI
- security controls
- carrier infrastructure
- Internet infrastructure
- cloud/edge infrastructure
- physical infrastructure
- monitoring
- investigation

That makes it an unusually efficient learning vehicle.

It also establishes a recurring pattern for the entire Atlas:

> **Something happens → trace the system → identify dependencies → identify trust → identify threats → build a model → break it → defend it → investigate it → explain it.**

---

# 6. SYSTEM ARCHITECTURE

The architecture will be explored through multiple zoom levels.

## LEVEL 0 — Human View

```
PHONE
  ↓
INTERNET
  ↓
GOOGLE
  ↓
WEBPAGE
```

At this level the goal is simply to establish the journey.

---

## LEVEL 1 — Major System View

```
Smartphone
    ↓
Cellular Radio Network
    ↓
Carrier Network
    ↓
Internet
    ↓
Google Infrastructure
    ↓
Response
```

Questions introduced:

- What is the cellular radio network?
- What is the carrier network?
- Where does the Internet begin?
- What exactly is "Google" from a networking perspective?

---

## LEVEL 2 — Network Architecture

```
┌───────────────┐
│ Smartphone    │
└───────┬───────┘
        │
      5G NR
        │
        ▼
┌───────────────┐
│ gNodeB / RAN  │
└───────┬───────┘
        │
    Transport
        │
        ▼
┌───────────────┐
│ Carrier Core  │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│ IP Network /  │
│ Internet      │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│ Google / Edge │
│ Infrastructure│
└───────────────┘
```

This is a conceptual architecture rather than a claim that every carrier implements the exact same physical topology.

---

## LEVEL 3 — Protocol View

The journey becomes a stack of interacting protocols and services.

```
Application
    │
HTTPS
    │
TLS
    │
TCP / QUIC
    │
IP
    │
Link / Ethernet / Cellular
    │
Physical / Radio
```

Alongside the primary flow:

```
Identity
Authentication
Authorization
DNS
Address Assignment
Routing
Security Controls
Logging / Monitoring
```

The precise protocol path will be investigated rather than assumed.

---

## LEVEL 4 — Infrastructure View

We zoom into actual components and interfaces.

Potential components include:

- smartphone modem
- antennas
- radio access equipment
- gNodeB
- transport links
- routers
- switches
- carrier core functions
- firewalls/security systems
- DNS infrastructure
- Internet routers
- peering/transit infrastructure
- Google edge infrastructure
- application servers/services

The mission does not require reproducing a real carrier network.

The goal is understanding the functions and relationships.

---

## LEVEL 5 — Evidence View

We now ask:

> **What evidence would prove that this actually happened?**

Potential evidence:

- DNS queries
- IP addresses
- packet captures
- TCP/QUIC behavior
- TLS handshakes
- certificate information
- routing information
- interface information
- logs
- timestamps
- connection states
- firewall events
- IDS/IPS events
- endpoint/network metadata
- vulnerability findings
- failure behavior

---

# 7. SYSTEM JOURNEY

The canonical journey we will eventually be able to explain is:

```
USER
 ↓
BROWSER
 ↓
SMARTPHONE OS
 ↓
NETWORK STACK
 ↓
CELLULAR MODEM
 ↓
5G RADIO
 ↓
gNodeB / RAN
 ↓
CARRIER TRANSPORT
 ↓
5G CORE
 ↓
CARRIER IP NETWORK
 ↓
INTERNET
 ↓
GOOGLE EDGE / SERVICE
 ↓
GOOGLE APPLICATION INFRASTRUCTURE
 ↓
RESPONSE
 ↓
RETURN PATH
 ↓
PHONE
 ↓
BROWSER
```

However, the journey will not be treated as one monolithic process.

It will be decomposed into questions and evidence.

---

# 8. CORE QUESTIONS

## Application

- What does the browser actually do?
- What happens when `google.com` is entered?
- How does the phone determine what service it is contacting?
- What application protocols are involved?

## Naming

- What is DNS?
- How does `google.com` become an address?
- Where does the DNS request go?
- What protects DNS?
- What happens if DNS is manipulated?

## Addressing

- What address does the phone have?
- Is it globally routable?
- What addresses exist at different layers?
- Where does NAT occur, if applicable?
- How does address assignment work?

## Cellular

- How does the phone communicate with the tower?
- What is 5G NR?
- What is a gNodeB?
- How does the phone select a cell?
- What happens while the phone is moving?
- How does cellular identity work?
- Where does cellular authentication occur?

## Carrier Network

- What happens after the radio signal reaches the tower?
- How does traffic travel through the carrier?
- What is the transport network?
- What is the carrier core?
- Where are identity and mobility functions involved?
- How is traffic separated?

## Routing

- How does traffic find its destination?
- What routers make decisions?
- What is a routing table?
- What happens when a route disappears?
- How can routing failures be distinguished from security-policy failures?

## Transport

- What is TCP?
- When is UDP used?
- Where does QUIC fit?
- What does a connection actually mean?
- How do loss and latency affect the application?

## Security

- Where does authentication happen?
- Where does authorization happen?
- How is confidentiality established?
- How is integrity protected?
- What does a certificate prove?
- What is PKI?
- Where are trust boundaries?
- Where could an attacker interfere?
- What security controls can be placed at each layer?

## Availability

- What happens if a link fails?
- What happens if a router fails?
- What happens if DNS becomes unavailable?
- What happens if the cellular connection changes?
- How does the system recover?
- What evidence identifies the failure?

## Evidence

- What can we observe?
- What can Wireshark show?
- What can logs show?
- What can vulnerability data show?
- What can we infer?
- What can we not prove from available evidence?

---

# 9. MISSION OPERATING MODEL

Mission 01 follows this cycle:

```
QUESTION
   ↓
ARCHITECTURE
   ↓
INVESTIGATION
   ↓
MODEL
   ↓
IMPLEMENTATION
   ↓
OBSERVATION
   ↓
FAILURE / ATTACK / CHANGE
   ↓
EVIDENCE
   ↓
MITIGATION
   ↓
VALIDATION
   ↓
EXPLANATION
   ↓
SECURITY+ MAPPING
```

The mission should not become a sequence of disconnected textbook lessons.

Each concept should enter because the system creates a reason to understand it.

---

# 10. SECURITY+ COVERAGE MODEL

## Coverage rule

Every Security+ atomic requirement must appear in the Atlas.

No requirement disappears because it does not fit Mission 01.

Mission 01 does not need to own every requirement.

It does need to account for every requirement.

The coverage status in this passport represents the **expected level of coverage by the time Mission 01 is complete**.

It does **not** represent current learner achievement.

---

## Coverage status vocabulary

|Status|Meaning|
|---|---|
|🟢 **Demonstrated**|Mission 01 is expected to produce practical evidence of the requirement.|
|🟡 **Understood**|Mission 01 is expected to produce explanation/application evidence, but not necessarily deep implementation.|
|🔵 **Encountered**|Mission 01 is expected to place the requirement in meaningful context, but deeper mastery belongs elsewhere.|
|⚪ **Not a Mission 01 Target**|The requirement is accounted for in the Atlas but deliberately not owned by Mission 01.|

These colors are **planned completion coverage**, not current status.

They must not be interpreted as evidence already earned.

---

# 11. SECURITY+ ATOMIC COVERAGE

## DOMAIN 1 — GENERAL SECURITY CONCEPTS

### 1.1 — Security Controls

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.1-A** Compare technical controls|🟢 Demonstrated|
|**1.1-B** Compare preventive controls|🟢 Demonstrated|
|**1.1-C** Compare managerial controls|🟡 Understood|
|**1.1-D** Compare deterrent controls|🟡 Understood|
|**1.1-E** Compare operational controls|🟢 Demonstrated|
|**1.1-F** Compare detective controls|🟢 Demonstrated|
|**1.1-G** Compare physical controls|🟡 Understood|
|**1.1-H** Compare corrective controls|🟢 Demonstrated|
|**1.1-I** Compare compensating controls|🟡 Understood|
|**1.1-J** Compare directive controls|🟡 Understood|

**Mission evidence:** security-control analysis, firewall/access-control work, monitoring, failure scenarios, physical/security architecture analysis, corrective and compensating control discussion.

---

### 1.2 — Fundamental Security Concepts

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.2-A** Summarize confidentiality|🟢 Demonstrated|
|**1.2-B** Summarize integrity|🟢 Demonstrated|
|**1.2-C** Summarize availability|🟢 Demonstrated|
|**1.2-D** Explain non-repudiation|🟡 Understood|
|**1.2-E** Explain authentication|🟢 Demonstrated|
|**1.2-F** Explain authorization|🟢 Demonstrated|
|**1.2-G** Explain accounting|🟡 Understood|
|**1.2-H** Explain Zero Trust|🟡 Understood|
|**1.2-I** Explain deception/disruption technology|🔵 Encountered|

---

### 1.3 — Change Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.3-A** Explain business processes associated with change management|🔵 Encountered|
|**1.3-B** Explain technical implications of changes|🟢 Demonstrated|
|**1.3-C** Explain change documentation|🟡 Understood|
|**1.3-D** Explain/use version control|🟡 Understood|

**Required scenario:**

> **Build → baseline → change → test → compare → document → rollback/version**

This prevents change management from becoming an artificial checkbox.

---

### 1.4 — Cryptographic Solutions

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.4-A** Use/understand PKI|🟢 Demonstrated|
|**1.4-B** Use/understand encryption|🟢 Demonstrated|
|**1.4-C** Understand obfuscation|🔵 Encountered|
|**1.4-D** Use/understand hashing|🟢 Demonstrated|
|**1.4-E** Use/understand digital signatures|🟡 Understood|
|**1.4-F** Understand blockchain|⚪ Not a Mission 01 Target|

---

# DOMAIN 2 — THREATS, VULNERABILITIES & MITIGATIONS

## 2.1 — Threat Actors and Motivations

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.1-A** Compare nation-state threat actors|🟡 Understood|
|**2.1-B** Compare unskilled attackers|🟡 Understood|
|**2.1-C** Compare hacktivists|🔵 Encountered|
|**2.1-D** Compare insider threats|🟡 Understood|
|**2.1-E** Compare organized crime|🟡 Understood|
|**2.1-F** Understand shadow IT as a threat/risk|🔵 Encountered|
|**2.1-G** Understand data exfiltration motivation|🟡 Understood|
|**2.1-H** Understand espionage motivation|🟡 Understood|
|**2.1-I** Understand financial gain motivation|🟡 Understood|

---

## 2.2 — Threat Vectors and Attack Surfaces

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.2-A** Explain message-based vectors|🔵 Encountered|
|**2.2-B** Explain unsecure network vectors|🟢 Demonstrated|
|**2.2-C** Explain social engineering vectors|🔵 Encountered|
|**2.2-D** Explain file-based vectors|🔵 Encountered|
|**2.2-E** Explain voice call vectors|🔵 Encountered|
|**2.2-F** Explain supply chain vectors|🟡 Understood|
|**2.2-G** Explain vulnerable software vectors|🟢 Demonstrated|
|**2.2-H** Identify/analyze relevant attack surfaces|🟢 Demonstrated|

**Required artifact:**

> **Actual attack-surface / threat-vector map**

The mission must distinguish theoretical attack surfaces from attacks actually reproduced.

---

## 2.3 — Vulnerabilities

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.3-A** Explain application vulnerabilities|🟢 Demonstrated|
|**2.3-B** Explain hardware vulnerabilities|🟡 Understood|
|**2.3-C** Explain mobile device vulnerabilities|🟢 Demonstrated|
|**2.3-D** Explain virtualization vulnerabilities|🔵 Encountered|
|**2.3-E** Explain OS-based vulnerabilities|🟢 Demonstrated|
|**2.3-F** Explain cloud-specific vulnerabilities|🟡 Understood|
|**2.3-G** Explain web-based vulnerabilities|🟢 Demonstrated|
|**2.3-H** Explain supply chain vulnerabilities|🟡 Understood|

---

## 2.4 — Malicious Activity

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.4-A** Analyze malware attacks|🟡 Understood|
|**2.4-B** Analyze password attacks|🟡 Understood|
|**2.4-C** Analyze application attacks|🟢 Demonstrated|
|**2.4-D** Analyze physical attacks|🟡 Understood|
|**2.4-E** Analyze network attacks|🟢 Demonstrated|
|**2.4-F** Analyze cryptographic attacks|🟡 Understood|

**Principle:**

> Analyze does not mean safely reproduce every attack.

Offensive activities remain controlled and confined to authorized laboratory environments.

---

## 2.5 — Mitigation Techniques

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.5-A** Apply segmentation|🟢 Demonstrated|
|**2.5-B** Apply access control|🟢 Demonstrated|
|**2.5-C** Apply configuration enforcement|🟢 Demonstrated|
|**2.5-D** Apply hardening|🟢 Demonstrated|
|**2.5-E** Apply isolation|🟢 Demonstrated|
|**2.5-F** Apply patching|🟡 Understood|

**Pressure-test conclusion:** this remains one of Mission 01's strongest practical areas.

---

# DOMAIN 3 — SECURITY ARCHITECTURE

## 3.1 — Architecture Models

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.1-A** Compare on-premises architecture|🟡 Understood|
|**3.1-B** Compare cloud architecture|🟡 Understood|
|**3.1-C** Compare virtualization architecture|🔵 Encountered|
|**3.1-D** Compare IoT architecture|🔵 Encountered|
|**3.1-E** Compare ICS architecture|🔵 Encountered|
|**3.1-F** Compare Infrastructure as Code|🔵 Encountered|

Mission 01 encounters and distinguishes these models.

It does not pretend to own their deep implementation.

---

## 3.2 — Enterprise Infrastructure

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.2-A** Apply security principles to infrastructure considerations|🟢 Demonstrated|
|**3.2-B** Apply security principles to control selection|🟢 Demonstrated|
|**3.2-C** Apply security principles to secure communication|🟢 Demonstrated|
|**3.2-D** Apply security principles to secure access|🟢 Demonstrated|

**Pressure-test conclusion:** very strong natural fit.

---

## 3.3 — Data Protection

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.3-A** Compare relevant data types|🟡 Understood|
|**3.3-B** Compare data securing methods|🟢 Demonstrated|
|**3.3-C** Understand general data protection considerations|🟡 Understood|
|**3.3-D** Apply data classifications|🔵 Encountered|

---

## 3.4 — Resilience and Recovery

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.4-A** Explain high availability|🟢 Demonstrated|
|**3.4-B** Explain site considerations|🟡 Understood|
|**3.4-C** Explain testing for resilience/recovery|🟢 Demonstrated|
|**3.4-D** Explain power considerations|🔵 Encountered|
|**3.4-E** Explain platform diversity|🟡 Understood|
|**3.4-F** Explain backups|🔵 Encountered|
|**3.4-G** Explain continuity of operations|🟡 Understood|

Mission 01 establishes resilience reasoning; deeper recovery belongs elsewhere.

---

# DOMAIN 4 — SECURITY OPERATIONS

## 4.1 — Computing Resources

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.1-A** Apply secure baselines|🟢 Demonstrated|
|**4.1-B** Apply security to mobile solutions|🟢 Demonstrated|
|**4.1-C** Apply hardening|🟢 Demonstrated|
|**4.1-D** Apply wireless security|🟢 Demonstrated|
|**4.1-E** Apply application security|🟢 Demonstrated|
|**4.1-F** Apply sandboxing|🟡 Understood|
|**4.1-G** Apply monitoring to computing resources|🟢 Demonstrated|

---

## 4.2 — Asset Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.2-A** Manage hardware/software/data acquisition|🔵 Encountered|
|**4.2-B** Manage asset disposal|⚪ Not a Mission 01 Target|
|**4.2-C** Manage asset assignment|🔵 Encountered|
|**4.2-D** Manage asset monitoring/tracking|🟡 Understood|

Mission 01 establishes the concepts; lifecycle ownership belongs elsewhere.

---

## 4.3 — Vulnerability Management

This receives full lifecycle treatment.

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.3-A** Identify vulnerabilities|🟢 Demonstrated|
|**4.3-B** Analyze vulnerabilities|🟢 Demonstrated|
|**4.3-C** Remediate vulnerabilities|🟢 Demonstrated|
|**4.3-D** Validate remediation|🟢 Demonstrated|
|**4.3-E** Report vulnerabilities|🟢 Demonstrated|

### Required evidence

> **Identify → Analyze → Remediate → Validate → Report**

A vulnerability scanner alone does not satisfy 4.3.

---

## 4.4 — Alerting and Monitoring

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.4-A** Explain/use monitoring tools|🟢 Demonstrated|
|**4.4-B** Explain computing resource activities relevant to monitoring|🟢 Demonstrated|

---

## 4.5 — Enterprise Security

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.5-A** Modify/configure firewalls|🟢 Demonstrated|
|**4.5-B** Use/configure IDS/IPS|🟡 Understood|
|**4.5-C** Use/configure DNS filtering|🟢 Demonstrated|
|**4.5-D** Use/configure DLP|🔵 Encountered|
|**4.5-E** Use/configure NAC|🔵 Encountered|
|**4.5-F** Use/configure EDR/XDR|🔵 Encountered|

Mission 01 must not artificially implement every enterprise security technology merely to generate a checkbox.

---

## 4.6 — Identity and Access Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.6-A** Implement provisioning|🔵 Encountered|
|**4.6-B** Implement SSO|🔵 Encountered|
|**4.6-C** Implement MFA|🟡 Understood|
|**4.6-D** Implement/use privileged access tools|🔵 Encountered|

Authentication and authorization are strong Mission 01 concepts, but Mission 01 is not the primary IAM implementation mission.

---

## 4.7 — Automation and Orchestration

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.7-A** Explain automation use cases|🟡 Understood|
|**4.7-B** Explain scripting benefits|🟡 Understood|
|**4.7-C** Explain automation considerations|🔵 Encountered|

Automation may support evidence collection, network analysis, configuration, and reporting without becoming the mission's central subject.

---

## 4.8 — Incident Response

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.8-A** Implement incident response processes|🟡 Understood|
|**4.8-B** Address incident response training|🔵 Encountered|
|**4.8-C** Conduct incident response testing|🟢 Demonstrated|
|**4.8-D** Perform root cause analysis|🟢 Demonstrated|
|**4.8-E** Conduct threat hunting|🟡 Understood|
|**4.8-F** Conduct/use digital forensics|🟢 Demonstrated|

Mission evidence comes from:

- failure reconstruction
- controlled security scenarios
- evidence preservation
- investigation
- timeline reconstruction
- root-cause analysis
- controlled incident-response testing

---

## 4.9 — Data Sources

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.9-A** Use log data to support investigations|🟢 Demonstrated|
|**4.9-B** Use other data sources to support investigations|🟢 Demonstrated|

Potential evidence includes:

- firewall logs
- application logs
- endpoint/OS logs
- IDS/IPS logs
- network logs
- metadata
- vulnerability scans
- automated reports
- dashboards
- packet captures
- certificate information
- DNS evidence
- timestamps

---

# DOMAIN 5 — SECURITY PROGRAM MANAGEMENT & OVERSIGHT

## 5.1 — Security Governance

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.1-A** Understand guidelines|🔵 Encountered|
|**5.1-B** Understand policies|🟡 Understood|
|**5.1-C** Understand standards|🟡 Understood|
|**5.1-D** Understand procedures|🟡 Understood|
|**5.1-E** Understand external considerations|🔵 Encountered|
|**5.1-F** Understand monitoring within governance|🔵 Encountered|
|**5.1-G** Understand governance structures|🔵 Encountered|
|**5.1-H** Understand roles/responsibilities|🟡 Understood|

---

## 5.2 — Risk Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.2-A** Perform/understand risk identification|🟢 Demonstrated|
|**5.2-B** Perform/understand risk assessment|🟢 Demonstrated|
|**5.2-C** Perform/understand risk analysis|🟢 Demonstrated|
|**5.2-D** Maintain/use a risk register|🟡 Understood|
|**5.2-E** Understand risk tolerance|🟡 Understood|
|**5.2-F** Understand risk appetite|🟡 Understood|
|**5.2-G** Select/apply risk strategies|🟢 Demonstrated|
|**5.2-H** Perform risk reporting|🟡 Understood|
|**5.2-I** Conduct/use a BIA|🔵 Encountered|

Risk is legitimate where the mission requires decisions about system exposure, controls, failure consequences, and mitigation.

Mission 01 is not the primary enterprise risk-management mission.

---

## 5.3 — Third-Party Risk

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.3-A** Conduct vendor assessment|⚪ Not a Mission 01 Target|
|**5.3-B** Conduct vendor selection|⚪ Not a Mission 01 Target|
|**5.3-C** Understand/manage vendor agreements|⚪ Not a Mission 01 Target|
|**5.3-D** Conduct vendor monitoring|⚪ Not a Mission 01 Target|
|**5.3-E** Use vendor questionnaires|⚪ Not a Mission 01 Target|
|**5.3-F** Establish/use rules of engagement|🔵 Encountered|

Mission 01 deliberately does not manufacture third-party-risk coverage.

---

## 5.4 — Security Compliance

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.4-A** Understand compliance reporting|🔵 Encountered|
|**5.4-B** Understand consequences of non-compliance|🔵 Encountered|
|**5.4-C** Conduct compliance monitoring|🔵 Encountered|
|**5.4-D** Understand/apply privacy considerations|🟡 Understood|

---

## 5.5 — Audits and Assessments

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.5-A** Understand attestation|🔵 Encountered|
|**5.5-B** Understand/participate in internal audits|🔵 Encountered|
|**5.5-C** Understand/participate in external audits|⚪ Not a Mission 01 Target|
|**5.5-D** Understand/use penetration testing|🟡 Understood|

---

## 5.6 — Security Awareness

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.6-A** Implement phishing training|⚪ Not a Mission 01 Target|
|**5.6-B** Recognize anomalous behavior|🟡 Understood|
|**5.6-C** Provide user guidance|🔵 Encountered|
|**5.6-D** Implement user reporting|🔵 Encountered|
|**5.6-E** Implement/use monitoring|🟡 Understood|

---

# 12. COVERAGE INTEGRITY RESULT

The pressure test produces the following architectural conclusion:

## The Atlas is complete.

Every atomic Security+ requirement is accounted for.

## Mission 01 is not expected to demonstrate every requirement.

That is intentional.

Mission 01's responsibility is to:

1. demonstrate the requirements naturally supported by the Phone → Google system;
2. establish meaningful understanding of adjacent requirements;
3. deliberately encounter requirements whose deeper treatment belongs elsewhere;
4. explicitly identify requirements that are not Mission 01 targets.

This prevents false coverage.

---

# 13. COVERAGE CLASS DEFINITIONS

## 🟢 Demonstrated

Mission 01 must produce practical evidence.

Typical evidence:

- working configuration
- packet capture
- system diagram
- controlled failure
- remediation
- validation
- investigation
- reconstructed behavior
- functioning security control
- technical report

---

## 🟡 Understood

Mission 01 must produce explanation/application evidence.

The learner must be able to explain the concept and apply it to the system.

---

## 🔵 Encountered

Mission 01 places the requirement into meaningful context.

The learner should recognize the concept and understand why it exists, but deeper mastery belongs elsewhere.

---

## ⚪ Not a Mission 01 Target

The requirement remains in the Atlas but Mission 01 deliberately does not own it.

No artificial lab should be created merely to change the color.

---

# 14. CONCEPTS TO DISCOVER

These are not a chapter list.

They are the conceptual territory expected to emerge while answering mission questions.

## Networking

- Ethernet
- switching
- routing
- IP addressing
- subnetting
- NAT
- DHCP
- DNS
- TCP
- UDP
- QUIC
- HTTP/HTTPS
- routing tables
- peering/transit

## Cellular

- RF
- 5G NR
- RAN
- gNodeB
- spectrum
- cells
- mobility
- handover
- cellular identity
- SIM/eSIM
- carrier core
- transport network

## Security

- authentication
- authorization
- accounting
- encryption
- hashing
- digital signatures
- certificates
- PKI
- TLS
- trust boundaries
- Zero Trust
- firewalls
- IDS/IPS
- DNS filtering
- monitoring
- vulnerability management
- incident response
- digital forensics

## Infrastructure

- fiber
- routers
- switches
- network interfaces
- data centers
- edge infrastructure
- power
- timing
- physical security

---

# 15. LABS

**Important:** These are planned labs. Nothing is considered executed merely because it appears here.

## Lab 01 — Build the Simplified Journey

Create:

```
Client
  ↓
Access Network
  ↓
Carrier/ISP Router
  ↓
Internet
  ↓
Web Server
```

Goal:

Understand the basic packet journey before adding complexity.

---

## Lab 02 — Build the Carrier-Like Network

Expand the model:

```
Client
   ↓
Access Network
   ↓
Aggregation
   ↓
Regional Router
   ↓
ISP Core
   ↓
Internet
   ↓
Destination
```

Introduce:

- interfaces
- addressing
- routing
- segmentation
- failure points
- security controls

---

## Lab 03 — DNS Investigation

Investigate:

```
Application
    ↓
DNS Query
    ↓
Resolver
    ↓
DNS Response
    ↓
Destination Address
```

Evidence:

- DNS queries
- responses
- addresses
- timing
- filtering behavior

---

## Lab 04 — Packet Capture

Use Wireshark or an equivalent controlled capture environment.

Investigate:

- packet structure
- addressing
- transport
- DNS
- TLS/QUIC behavior
- timing
- connection states

---

## Lab 05 — TLS Investigation

Inspect a real or controlled HTTPS connection.

Investigate:

- certificates
- certificate chains
- trust
- encryption
- authentication
- integrity
- TLS negotiation
- digital signatures

---

## Lab 06 — Routing Failure

Deliberately remove or disable a route in the simulated environment.

Observe:

- loss of connectivity
- routing behavior
- convergence
- alternate paths where configured
- evidence of failure

---

## Lab 07 — Firewall / Access Control

Implement controlled security policies.

Ask:

> What traffic should be allowed, denied, logged, or inspected?

Then test the policy.

---

## Lab 08 — DNS Attack Scenario

Within the isolated lab, model a DNS manipulation scenario.

Investigate:

- what changes
- what evidence appears
- what security control could detect/prevent it
- how the user experience changes

---

## Lab 09 — Vulnerability Lifecycle

Introduce a controlled vulnerability into the lab.

Complete:

```
IDENTIFY
   ↓
ANALYZE
   ↓
REMEDIATE
   ↓
VALIDATE
   ↓
REPORT
```

This lab exists specifically to prevent 4.3 from being reduced to "run a scanner."

---

## Lab 10 — Monitoring and Investigation

Generate controlled activity and investigate it using multiple evidence sources.

Correlate:

- logs
- packet captures
- timestamps
- network metadata
- endpoint information
- security-tool output

---

## Lab 11 — Incident Reconstruction

Given evidence rather than a diagram, reconstruct what happened.

Produce:

- timeline
- affected components
- root cause
- evidence supporting the conclusion
- security controls involved
- recommended remediation

---

## Lab 12 — End-to-End Reconstruction

Given evidence rather than a diagram, reconstruct the complete Phone → Google journey.

This becomes one of the first true systems-engineering exercises.

---

# 16. FAILURE SCENARIOS

## Failure A — DNS unavailable

> Can the user reach the destination if name resolution fails?

---

## Failure B — Route disappears

> What happens when the preferred path disappears?

---

## Failure C — Firewall rule blocks traffic

> How do we distinguish a security-policy failure from a network failure?

---

## Failure D — Cellular connectivity changes

> What happens when the phone moves between cells?

---

## Failure E — High latency

> How do we determine where latency was introduced?

---

## Failure F — Packet loss

> How does packet loss affect the application?

---

## Failure G — Certificate/trust failure

> What happens when the client cannot establish trust?

---

## Failure H — Vulnerable component discovered

> How do we identify, analyze, remediate, validate, and report the vulnerability?

---

## Failure I — Suspicious network activity

> Can we reconstruct what happened from available evidence?

---

# 17. ATTACK SCENARIOS

The architecture will consider:

- rogue/unauthorized wireless infrastructure
- DNS manipulation
- credential theft
- malicious network traffic
- application vulnerabilities
- man-in-the-middle concepts
- denial/disruption
- physical compromise
- insecure configuration
- vulnerable software

The distinction between:

**attack concept → safe simulation → actual reproduction**

will be maintained throughout the Atlas.

Offensive activities remain controlled and authorized.

---

# 18. TANGIBLE ARTIFACTS

Mission 01 will ultimately produce:

1. **Level 0 architecture diagram**
2. **Level 1 architecture diagram**
3. **Level 2 carrier architecture**
4. **Detailed packet-flow diagram**
5. **Protocol-stack diagram**
6. **Trust-boundary diagram**
7. **Attack-surface map**
8. **Threat-vector map**
9. **Simplified network topology**
10. **DNS investigation evidence**
11. **Packet captures**
12. **TLS/certificate analysis**
13. **Routing-failure analysis**
14. **Firewall/security-policy configuration**
15. **Security-control analysis**
16. **Vulnerability lifecycle evidence**
17. **Monitoring evidence**
18. **Incident reconstruction**
19. **Root-cause analysis**
20. **Risk analysis**
21. **Mission 01 technical report**
22. **Security+ atomic coverage record**
23. **Final "Phone → Google" explanation**

The final explanation is itself an artifact.

---

# 19. EVIDENCE OF LEARNING

The learner's **actual state** is tracked separately from the passport's **planned completion coverage**.

The Atlas status vocabulary remains:

|Status|Meaning|
|---|---|
|⚪|Not encountered|
|🔵|Encountered|
|🟡|Understood|
|🟢|Demonstrated|
|🟣|Exam verified|

The passport's coverage table does **not** pre-award these states.

For example:

> A requirement marked 🟢 in the passport means Mission 01 is designed to produce demonstration evidence.

It does **not** mean the learner has already demonstrated it.

The actual Atlas record changes only when evidence exists.

---

# 20. SECURITY+ COVERAGE VS. LEARNER STATE

This distinction is mandatory.

### Passport

Answers:

> **What should Mission 01 cover by completion?**

### Atlas evidence record

Answers:

> **What has the learner actually demonstrated?**

Therefore:

```
PLANNED MISSION COVERAGE
        ≠
CURRENT LEARNER EVIDENCE
```

A mission can be designed to demonstrate something and still have zero evidence because the mission has not been executed.

---

# 21. FAILURE / ATTACK / CHANGE DISCIPLINE

Every deliberate modification should follow a controlled cycle:

```
BASELINE
   ↓
CHANGE
   ↓
OBSERVE
   ↓
DOCUMENT
   ↓
ANALYZE
   ↓
RESTORE
   ↓
VALIDATE
```

Security incidents follow a related cycle:

```
EVENT
   ↓
PRESERVE EVIDENCE
   ↓
INVESTIGATE
   ↓
RECONSTRUCT
   ↓
ROOT CAUSE
   ↓
MITIGATE
   ↓
VALIDATE
   ↓
REPORT
```

This gives Mission 01 legitimate connections to change management, vulnerability management, monitoring, incident response, forensics, and risk.

---

# 22. OPEN QUESTIONS

The following questions should drive the investigation:

24. What exactly happens between pressing Enter and the DNS request?
25. Where does DNS resolution occur?
26. What address does the phone actually use?
27. How does the phone attach to the cellular network?
28. What does the gNodeB actually do?
29. What happens inside the carrier transport network?
30. What does the 5G core do?
31. Where does authentication occur?
32. How is the user's traffic separated from other users?
33. Where does routing occur?
34. Where does NAT occur, if applicable?
35. How does traffic reach the Internet?
36. How does Google receive the traffic?
37. How does HTTPS establish trust?
38. What does the certificate prove?
39. Where does encryption begin?
40. What happens if a router fails?
41. What happens if DNS fails?
42. What happens if the cellular connection changes?
43. What evidence can we capture?
44. Which Security+ controls are actually visible?
45. Which Security+ concepts remain only theoretical?
46. Which concepts require targeted verification labs?
47. What evidence would distinguish a network failure from a security control failure?
48. What evidence would allow reconstruction of an event after the fact?
49. How can a discovered vulnerability be tracked through remediation?
50. How can we validate that a mitigation actually worked?

---

# 23. CURIOSITY BRANCHES

Potential branches include:

## Cellular

- 5G NR
- spectrum
- antennas
- beamforming
- gNodeB architecture
- handovers
- SIM/eSIM
- cellular authentication
- carrier core

## Infrastructure

- fiber optics
- SFPs
- timing
- GPS/PTP
- tower equipment
- power systems
- batteries
- environmental monitoring
- microwave backhaul

## Networking

- BGP
- OSPF
- MPLS
- carrier Ethernet
- Internet exchange points
- peering
- transit
- CDN architecture

## Security

- TLS
- PKI
- certificate authorities
- DNSSEC
- encrypted DNS
- Zero Trust
- mobile security
- rogue base stations
- IDS/IPS
- DNS filtering
- endpoint security

## Google

- edge networks
- CDNs
- load balancing
- distributed systems
- data centers
- service architecture

---

# 24. DEFERRED TOPICS

These are intentionally captured rather than allowed to derail the mission.

Initial candidates:

- detailed BGP route-selection mechanics
- deep 5G radio engineering
- orbital/satellite networking
- advanced optical transport
- detailed carrier-core implementation
- Google's private internal infrastructure
- advanced timing protocols
- blockchain
- advanced cryptographic mathematics
- deep enterprise IAM
- deep vendor management
- enterprise audit mechanics
- detailed DLP implementation
- detailed NAC implementation
- detailed EDR/XDR implementation

A deferred topic can become active if it becomes necessary to answer a mission question.

Otherwise it remains deferred.

---

# 25. PRESSURE-TEST FINDINGS

The revised system journey is particularly strong for:

- security controls
- CIA
- authentication
- authorization
- cryptography
- network security
- attack surfaces
- vulnerabilities
- mitigation
- secure communication
- secure access
- mobile security
- application security
- secure baselines
- hardening
- wireless security
- monitoring
- vulnerability management
- firewall/DNS controls
- evidence collection
- packet analysis
- incident investigation
- root-cause analysis
- data sources
- risk analysis

The journey provides legitimate context for many other Security+ concepts without pretending to be their primary mission.

---

# 26. WHAT THE PRESSURE TEST REJECTED

Mission 01 will **not** artificially expand itself to demonstrate:

- blockchain
- deep cloud vulnerability implementation
- deep virtualization vulnerability implementation
- deep supply-chain implementation
- DLP implementation
- NAC implementation
- EDR/XDR implementation
- vendor management
- vendor questionnaires
- external audits
- attestation
- BIA
- deep governance structures
- phishing-training implementation
- advanced radio engineering
- Google's private internal architecture

These remain represented in the Atlas and can be owned by other missions or targeted Security+ Verification Labs.

---

# 27. NEXT MISSION CONNECTIONS

Mission 01 is intentionally foundational.

It establishes vocabulary and systems reasoning that later missions can reuse without reteaching the underlying concepts from scratch.

Potential connections include:

### Mission 02 — Starlink

Extends:

- wireless communications
- satellite networking
- routing
- distributed infrastructure
- resilience
- availability
- physical security
- alternative communication paths

### Mission 03 — Secure Innovation Lab

Extends:

- network architecture
- segmentation
- access control
- firewalls
- monitoring
- secure baselines
- vulnerability management

### Mission 06 — Drone ISR

Extends:

- wireless
- mobility
- secure communications
- availability
- authentication
- resilience

Mission 01 therefore acts as a foundational systems vocabulary builder without becoming a prerequisite for every later mission.

---

# 28. CURRENT STATE

**Mission status:** Not started.

**Architecture status:** Defined at conceptual level.

**Security+ coverage design:** Pressure-tested.

**Atomic requirements:** All accounted for.

**Planned completion coverage:** Defined.

**Labs:** Designed, not executed.

**Artifacts:** None produced yet.

**Security+ evidence:** None yet.

**Learner state:** Not pre-awarded.

---

# 29. WHAT WE KNOW

At mission launch, we know the intended architecture and learning objectives.

We do **not** assume that understanding the architecture on paper constitutes demonstrated knowledge.

The mission begins with the question.

---

# 30. WHAT WE HAVE BUILT

The mission architecture and learning design have been built.

The laboratory implementation has not.

The first implementation artifact will be the simplified representation of the journey.

---

# 31. NEXT RECOMMENDED ACTION

**Do not configure anything yet.**

First establish the **Level 0 → Level 1 architecture together** and identify the first unknowns.

The first question remains:

> **When I press Enter on `google.com`, what is the very first thing my phone has to know or do before it can send the request toward Google?**

That question determines the first conceptual branch of the mission.

---

# 32. MISSION COMPLETE WHEN

Mission 01 is complete only when:

- the end-to-end architecture can be drawn
- the system journey can be explained
- the major protocols can be explained
- the major trust relationships can be explained
- relevant Security+ concepts can be applied
- selected traffic can be investigated
- the simplified system has been built
- selected failures have been introduced
- security controls have been applied
- evidence has been analyzed
- vulnerabilities have been taken through an appropriate lifecycle
- selected incidents have been reconstructed
- root causes have been identified
- tangible artifacts have been produced
- the learner can explain the complete journey independently
- Security+ atomic evidence has been recorded
- remaining gaps have been identified
- unresolved Security+ gaps have been assigned to later missions or Verification Labs

---

# 33. HANDOFF NOTES FOR ANOTHER AI

**Do not restart this mission from scratch.**

The learner is using a systems-journey learning model.

The destination is **CompTIA Security+ V7**.

The mission is **Mission 01 — How Does My Phone Reach Google?**

The learner prefers understanding systems by tracing real events end-to-end rather than studying concepts in arbitrary textbook order.

Do not turn this into a generic networking course.

Do not introduce Packet Tracer or other execution prematurely.

The mission begins in the **architecture phase**.

The next useful action is to investigate the first step of the journey and progressively refine the architecture.

When a concept is encountered, map it to the Security+ atomic matrix.

When a concept is expected to be demonstrated, require evidence before awarding the corresponding learner status.

When curiosity creates a valuable but nonessential branch, record it under **Curiosity Branches** or **Deferred Topics**.

Do not mark an objective demonstrated merely because the passport says the mission is designed to demonstrate it.

Do not expand Mission 01 with new major activities solely to turn an inconvenient Security+ requirement green.

Use a targeted **Security+ Verification Lab** when necessary.

The governing principle remains:

> **Security+ is the destination. The Mission Atlas is the vehicle.**

---

# 34. ARCHITECTURAL FREEZE

This version incorporates the final pressure-test decisions.

The following are considered **frozen design principles** for the Atlas unless deliberately reopened:

1. **Every Security+ atomic requirement remains represented in the Atlas.**
2. **Mission passports use atomic Security+ coverage rather than separate parent-level coverage.**
3. **Mission coverage represents intended coverage by mission completion, not current learner achievement.**
4. **Coverage uses four planning classes: Demonstrated, Understood, Encountered, Not a Mission Target.**
5. **Actual learner evidence uses the separate five-state Atlas vocabulary: ⚪ 🔵 🟡 🟢 🟣.**
6. **Mission ownership is not the same thing as Atlas coverage.**
7. **A mission is not expanded artificially to accommodate poorly fitting objectives.**
8. **Verification Labs are legitimate mechanisms for closing Security+ gaps.**
9. **4.8 Incident Response and 4.9 Data Sources remain separate objectives.**
10. **Labs are planned until actually executed.**
11. **Artifacts are not considered produced until they actually exist.**
12. **A future AI should use this passport as the authoritative Mission 01 design rather than reconstructing the mission from conversation history.**

---

## FINAL GOVERNING PRINCIPLE

> **Security+ is the destination.**
>
> **The Mission Atlas is the vehicle.**
>
> **The missions are real systems to investigate, build, break, defend, and explain.**
>
> **Coverage is planned. Evidence is earned. Nothing is assumed.**

---

# PART 3 — ATLAS ARCHITECTURE GOVERNANCE

## Frozen Design

The Security+ Mission Atlas architecture is considered **frozen at the structural level**.

The following are established design decisions and must not be casually redesigned:

- The **Security+ atomic requirements matrix** is the authoritative universe of requirements.
- The **Mission Atlas Register** is the authoritative cross-mission ownership and coverage map.
- Each mission has a **Mission Passport** using the established Passport structure.
- Mission Passports are the detailed execution plans for individual system journeys.
- Mission Passports contain their own labs, artifacts, curiosity branches, deferred topics, and mission-specific coverage.
- Tangible portfolio deliverables belong in the individual Mission Passports rather than being duplicated in the Atlas Register.
- The Atlas uses **cross-mission concept ownership and crossover** rather than forcing every concept into one mission.
- Security+ coverage is evaluated **in aggregation across the Atlas**, not by requiring every mission to cover every requirement.
- **Verification Labs** may be used to close Security+ gaps that are not naturally demonstrated by a primary mission.
- A mission should not be created merely because an interesting technology or Security+ requirement exists.
- The existing missions should not be expanded merely to make them appear more comprehensive.

## What May Change

The frozen architecture does **not** mean the content can never change.

As the missions are pressure-tested and executed, new evidence may justify:

- adding or modifying a lab;
- refining a mission's system journey;
- moving a requirement's primary ownership;
- identifying a new crossover between missions;
- adding a Verification Lab;
- recording a newly discovered gap;
- adding a curiosity branch;
- refining an artifact or evidence requirement;
- creating a new mission **if the Atlas demonstrates that one is genuinely necessary**.

Such changes should be made because of evidence, not because a concept merely seems interesting.

## New Ideas and Technologies

When a new idea appears, first ask:

1. **Does it naturally belong inside an existing mission?**
2. **Is it better treated as a curiosity branch or deferred topic?**
3. **Does it belong in a targeted Verification Lab?**
4. **Does another existing mission already provide a better context?**
5. **Does the Atlas reveal an actual Security+ coverage gap?**
6. **Only then: does the idea justify a new mission?**

For example, if the learner asks:

> "What happens when I press Send on an email?"

Do **not** automatically create an Email Mission.

First determine whether email can be handled as:

- a curiosity branch;
- a comparative system journey;
- a targeted investigation;
- a Verification Lab;
- or an extension of an existing mission.

Create a new mission only if the evidence shows that email represents a sufficiently valuable independent system journey that cannot be handled appropriately by the existing architecture.

## Evidence Over Intended Coverage

A mission's planned coverage is **not proof of learning**.

The Passport may state that a mission is expected to address a requirement. That is a design intention.

During execution, the AI must distinguish between:

**planned coverage**

and

**evidenced coverage**.

The final question is not:

> "Did we put this concept in the mission?"

The final question is:

> **"Did the completed work produce sufficient evidence to support the claimed Security+ coverage?"**

If the answer is no, the correct response is to identify the gap and determine whether it should be:

- addressed by another mission;
- addressed by an additional lab;
- addressed by a Verification Lab;
- or explicitly left for later.

Do not retroactively claim coverage simply because the concept appeared in the Passport.

## Change-Control Rule

Before proposing a structural change to the Atlas, the AI should distinguish:

**FROZEN ARCHITECTURE**
from
**EVOLVING CONTENT**.

Do not redesign the Atlas merely because a different structure appears attractive.

Do not add missions merely because additional topics are interesting.

Do not remove existing missions merely because their coverage overlaps.

Do not force artificial activities into missions solely to satisfy Security+ requirements.

Instead, preserve the architecture and improve the evidence.

## Governing Principle

> **The Atlas is the architecture. The Passports are the missions. The labs produce evidence. The Security+ matrix defines the requirements. Execution determines whether the intended coverage was actually achieved.**

The objective is not maximum breadth.

The objective is **credible, transferable, demonstrable Security+ competence produced through interesting real-world system journeys.**