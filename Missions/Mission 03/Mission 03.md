# MISSION PASSPORT

# MISSION: 03 — Build The Secure Innovation Lab

## VERSION: 1.0 — Architecture Draft

## STATUS: Designed / Not Executed

## DESTINATION: CompTIA Security+ V7

---

## 1. DESTINATION

CompTIA Security+ V7

Mission 03 is designed to demonstrate specific Security+ objectives through enterprise security architecture and control implementation. All atomic requirements are accounted for in the Atlas Register. This Passport must align with the master coverage map.

Cost Constraint: All labs executable with 100% free tools (GNS3, Packet Tracer, Wireshark, public resources).

---

## 2. MISSION INTENT

Understand how to build and secure an enterprise network infrastructure from the ground up.

The mission begins with this practical question:

"What would a minimally secure enterprise network look like, and how do I implement it?"

The objective is to develop the ability to:

|Skill|Purpose|
|---|---|
|Design secure network architecture|Understand defense-in-depth|
|Implement access controls|Learn identity and permissions|
|Configure firewalls and security controls|Hands-on perimeter security|
|Segment networks logically|Apply Zero Trust principles|
|Deploy monitoring systems|Detect and investigate anomalies|
|Establish secure baselines|Harden systems systematically|
|Document security policies|Translate requirements to procedures|
|Test security controls|Validate effectiveness|
|Apply change management|Maintain security during evolution|
|Automate security configurations|Scale protection efficiently|
|Map demonstrated knowledge to Security+|Produce exam-ready evidence|
|Produce tangible evidence of learning|Portfolio artifacts|

Security+ concepts will be introduced when they become necessary to answer questions about the enterprise system.

---

## 3. SCENARIO

A startup organization ("Innovation Lab") is establishing its first IT infrastructure.

The organization has:

- Limited budget (free/open-source tools preferred)
- Growing employee count (starting ~20 employees)
- Mixed device types (workstations, servers, mobile devices)
- Cloud and on-premises presence
- Compliance considerations (basic data protection)

The mission is to design and implement a secure network infrastructure that:

`USER DEVICES ↓ ACCESS NETWORK (VLANs, NAC concepts) ↓ SEGMENTATION ZONES (DMZ, internal, management) ↓ FIREWALLS & FIREWALL POLICIES ↓ IDS/IPS SYSTEMS ↓ MONITORING & LOGGING ↓ IDENTITY MANAGEMENT ↓ SECURE CONFIGURATIONS ↓ BACKUP & RECOVERY`

This contrasts with Mission 01 (consumption) and Mission 02 (satellite analysis) by focusing on building secure infrastructure deliberately.

---

## 4. END STATE

Mission 03 is complete when the learner can independently:

|Competency|Evidence Required|
|---|---|
|Design secure network topology|Documented architecture diagrams|
|Configure firewalls with security policies|Working GNS3/Packet Tracer configs|
|Implement network segmentation|VLAN/VRF configurations with evidence|
|Deploy IDS/IPS rules|Signature configurations and alerts|
|Configure access controls (IAM basics)|User/group assignments documented|
|Apply secure baselines to systems|Hardening checklists with before/after|
|Implement monitoring solutions|Log collection and analysis artifacts|
|Document security policies/procedures|Written policy documents|
|Test security control effectiveness|Validation test results|
|Implement DNS filtering concepts|Configuration documentation|
|Apply automation for security configs|Script artifacts|
|Map demonstrated knowledge to Security+|Coverage matrix update|
|Produce tangible evidence of learning|Portfolio artifacts|
|Explain the complete system coherently|Narrative without script|

---

## 5. WHY THIS MISSION EXISTS

This mission serves specific purposes that Mission 01 and 02 do not cover:

|Purpose|How Mission 03 Delivers|
|---|---|
|Enterprise security architecture|Multi-zone, multi-control design|
|Hands-on control implementation|Configure real (simulated) security devices|
|Defense-in-depth practice|Layered security approach|
|Access control depth|IAM, provisioning, permissions|
|Network security controls|Firewalls, IDS/IPS, DNS filtering, NAC|
|Policy documentation|Translate concepts to written procedures|
|Hardening practices|System-by-system security configuration|
|Change management|Controlled modifications to running systems|
|GNS3/Packet Tracer compatibility|Nearly 100% executable with free tools|

Security+ Domain 3.2 (Enterprise Infrastructure), 4.5 (Enterprise Security), 1.1 (Security Controls), and 5.1 (Security Governance) all receive primary treatment here.

---

## 6. SYSTEM ARCHITECTURE

Exploration occurs across multiple zoom levels:

### LEVEL 0 — Business View

`COMPANY ↓ EMPLOYEES ↓ NETWORK ↓ APPLICATIONS ↓ DATA`

### LEVEL 1 — Major Zone View

`┌─────────────────────────────────────────────────────────┐ │ ENTERPRISE NETWORK │ │ │ │ INTERNET → FIREWALL → DMZ → INTERNAL → DATABASE │ │ ↓ ↓ ↓ ↓ │ │ IDS/IPS MONITOR ACCESS BACKUPS │ └─────────────────────────────────────────────────────────┘`

### LEVEL 2 — Detailed Architecture

`┌──────────────────────────────────────────────────────────────┐ │ PERIMETER LAYER │ │ • Edge Firewall (stateful packet inspection) │ │ • IDS/IPS sensor │ │ • NAT translation │ │ • ISP connection │ ├──────────────────────────────────────────────────────────────┤ │ DMZ LAYER │ │ • Web server(s) │ │ • Mail server(s) │ │ • DNS server(s) │ │ • Restricted inbound access │ ├──────────────────────────────────────────────────────────────┤ │ INTERNAL LAYER │ │ • User workstations │ │ • File servers │ │ • Application servers │ │ • Active Directory/Identity Management │ │ • Internal VLANs │ ├──────────────────────────────────────────────────────────────┤ │ MANAGEMENT LAYER │ │ • Network management systems │ │ • SIEM/log collection │ │ • Backup servers │ │ • Administrative access only │ └──────────────────────────────────────────────────────────────┘`

Key concepts to discover:

- Why DMZ separation matters
- How firewall rules enforce segmentation
- Where logging should occur
- How access control flows through the architecture
- What monitoring reveals about system health

### LEVEL 3 — Security Control Stack

`Physical Security ↓ Perimeter Firewall ↓ Network Segmentation (VLANs/VRFs) ↓ Host-Based Security (EDR/Antivirus) ↓ Identity & Access Management ↓ Application Security ↓ Data Protection ↓ Monitoring & Detection`

Alongside the primary flow:

- Authentication mechanisms
- Authorization policies
- Logging requirements
- Encryption in transit/at rest
- Patch management
- Backup schedules
- Incident response readiness

### LEVEL 4 — Implementation Components

`┌────────────────────────────────────────────────────────┐ │ NETWORK INFRASTRUCTURE (GNS3/Packet Tracer) │ │ • Routers (multi-interface) │ │ • Switches (VLAN-capable) │ │ • Firewalls (ASA/iptables/OpenWrt) │ │ • IDS/IPS sensors │ ├────────────────────────────────────────────────────────┤ │ HOST SYSTEMS (Virtual Machines) │ │ • Windows/Linux workstations │ │ • Web server (Apache/Nginx) │ │ • File server │ │ • Domain controller/identity server │ ├────────────────────────────────────────────────────────┤ │ SECURITY TOOLS (Free/Open Source) │ │ • Snort/Suricata (IDS/IPS) │ │ • OSSEC/Wazuh (HIDS) │ │ • pfSense/OPNsense (firewall) │ │ • Splunk Free (logging) │ │ • Wireshark (packet capture) │ └────────────────────────────────────────────────────────┘`

### LEVEL 5 — Evidence View

What proves security controls are implemented?

- Firewall rule exports
- Network topology diagrams
- Configuration files with version history
- Log samples from monitoring systems
- Vulnerability scan results
- Policy documents signed/approved
- Change management tickets
- Access control lists
- Backup success logs
- Test results validating controls

---

## 7. SYSTEM JOURNEY

The canonical journey for this mission:

`BUSINESS REQUIREMENTS ↓ THREAT ASSESSMENT ↓ ARCHITECTURE DESIGN ↓ NETWORK IMPLEMENTATION ↓ SEGMENTATION CONFIGURATION ↓ FIREWALL POLICY CREATION ↓ HOST HARDENING ↓ IDENTITY SETUP ↓ MONITORING DEPLOYMENT ↓ POLICY DOCUMENTATION ↓ CONTROL TESTING ↓ VALIDATION & REVISION ↓ OPERATIONAL READINESS ↓ DOCUMENTED EVIDENCE ↓ SECURITY+ COVERAGE RECORD`

This decomposition becomes the investigation framework.

---

## 8. CORE QUESTIONS

### Architecture Design

- What zones does an enterprise network need?
- Why separate DMZ from internal systems?
- How much segmentation is enough?
- What happens if one zone is compromised?

### Network Implementation

- Which protocols run on each segment?
- How does traffic flow between zones?
- Where do routing decisions occur?
- How is broadcast traffic contained?

### Security Controls

- What firewall rules protect each zone?
- Where should IDS/IPS sensors be placed?
- How is DNS filtered or monitored?
- What access controls limit lateral movement?

### Identity Management

- How are users authenticated?
- Who authorizes access to resources?
- What accounts need elevated privileges?
- How is password policy enforced?

### Host Security

- What hardening steps apply to workstations?
- Which services should run on servers?
- How are patching and updates managed?
- What antivirus/EDR protection exists?

### Monitoring

- What logs should be collected?
- How long should logs be retained?
- Who reviews logs regularly?
- What triggers alerts?

### Policies

- What security policies are required?
- How are policies communicated to users?
- Who enforces policy compliance?
- How often are policies reviewed?

### Testing

- How do I verify firewall rules work?
- Can I test intrusion detection?
- How do I validate segmentation?
- What constitutes control effectiveness?

### Change Management

- How are changes documented before implementation?
- Who approves configuration changes?
- How do I rollback failed changes?
- What version control applies?

---

## 9. MISSION OPERATING MODEL

Mission 03 follows this cycle:

`REQUIREMENTS ↓ DESIGN ↓ IMPLEMENTATION ↓ CONFIGURATION ↓ DOCUMENTATION ↓ TESTING ↓ VALIDATION ↓ POLICY CREATION ↓ CHANGES ↓ RE-TESTING ↓ EVIDENCE COLLECTION ↓ SECURITY+ MAPPING`

Mission 03 differs from Mission 01 and 02 by emphasizing:

- Construction over consumption (building vs. tracing)
- Control implementation over analysis (doing vs. investigating)
- Policy creation over observation (writing vs. studying)
- GNS3/Packet Tracer hands-on work (nearly 100% executable)

---

## 10. SECURITY+ COVERAGE MODEL

Coverage rule (per Atlas): Every Security+ atomic requirement must appear in the Atlas. Mission 03 does not need to own every requirement—it needs to account for each and define its expected contribution.

Coverage status represents expected completion coverage, not learner achievement.

### Status Vocabulary (Mission 03 Completion)

|Status|Meaning|
|---|---|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|Practical evidence expected from Mission 03|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|Explanation/application evidence, less implementation|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|Contextual understanding; deeper ownership elsewhere|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 03 Target|Accounted in Atlas; deliberately not owned here|

---

## 11. SECURITY+ ATOMIC COVERAGE TABLE

### DOMAIN 1 — GENERAL SECURITY CONCEPTS

|Requirement|Mission 03 Completion|Rationale|
|---|---|---|
|1.1-A Technical controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Firewalls, IDS/IPS, segmentation|
|1.1-B Preventive controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|ACLs, hardening, authentication|
|1.1-C Managerial controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Policies, procedures, governance docs|
|1.1-D Deterrent controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Signage, access logs, surveillance|
|1.1-E Operational controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Procedures, training, monitoring ops|
|1.1-F Detective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IDS/IPS, SIEM, log monitoring|
|1.1-G Physical controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Datacenter security concepts|
|1.1-H Corrective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Patching, recovery, restore testing|
|1.1-I Compensating controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Alternative protections discussed|
|1.1-J Directive controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Policy documentation|
|1.2-A Confidentiality|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Access controls, encryption|
|1.2-B Integrity|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|File integrity monitoring|
|1.2-C Availability|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Redundancy, backups, HA concepts|
|1.2-D Non-repudiation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Minimal focus|
|1.2-E Authentication|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM setup, MFA concepts|
|1.2-F Authorization|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Role-based access control|
|1.2-G Accounting|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Logging, audit trails|
|1.2-H Zero Trust|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Segmentation, least privilege|
|1.2-I Deception/disruption|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M06 ownership|
|1.3-A Change mgmt processes|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Documented procedures|
|1.3-B Technical implications|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Before/after configurations|
|1.3-C Change documentation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Version-controlled configs|
|1.3-D Version control|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Git/config management|
|1.4-A PKI|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Certificate deployment concepts|
|1.4-B Encryption|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|TLS, disk encryption|
|1.4-C Obfuscation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|1.4-D Hashing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|File integrity concepts|
|1.4-E Digital signatures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M05/M07 ownership|
|1.4-F Blockchain|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target|Verification Lab reserved|

### DOMAIN 2 — THREATS, VULNERABILITIES & MITIGATIONS

|Requirement|Mission 03 Completion|Rationale|
|---|---|---|
|2.1-A Nation-state actors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.1-B Unskilled attackers|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Common misconfigurations|
|2.1-C Hacktivists|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.1-D Insider threats|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Access control mitigation|
|2.1-E Organized crime|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M08 ownership|
|2.1-F Shadow IT|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Policy enforcement|
|2.1-G Data exfiltration|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05 ownership|
|2.1-H Espionage|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M06/M08 ownership|
|2.1-I Financial gain|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M08 ownership|
|2.2-A Message-based vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M08 ownership|
|2.2-B Unsecure network vectors|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Firewall rules, segmentation|
|2.2-C Social engineering|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.2-D File-based vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05 ownership|
|2.2-E Voice call vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M06/M08 ownership|
|2.2-F Supply chain vectors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Software procurement policies|
|2.2-G Vulnerable software|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Patching, vulnerability management|
|2.2-H Attack surfaces|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Architecture analysis|
|2.3-A Application vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M04/M07 ownership|
|2.3-B Hardware vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06/M02/M04 ownership|
|2.3-C Mobile device vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06/M01 ownership|
|2.3-D Virtualization vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Hypervisor security|
|2.3-E OS-based vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Host hardening|
|2.3-F Cloud-specific vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07/M05 ownership|
|2.3-G Web-based vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M04 ownership|
|2.3-H Supply chain vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Procurement policies|
|2.4-A Malware attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M07 ownership|
|2.4-B Password attacks|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Policy enforcement, MFA|
|2.4-C Application attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M04 ownership|
|2.4-D Physical attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06/M02/M04 ownership|
|2.4-E Network attacks|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Firewall/IDS/IPS testing|
|2.4-F Cryptographic attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M04/M05 ownership|
|2.5-A Segmentation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|VLANs, DMZ, VRF implementation|
|2.5-B Access control|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|RBAC, ACLs configured|
|2.5-C Configuration enforcement|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Hardened baselines|
|2.5-D Hardening|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Host/system hardening|
|2.5-E Isolation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Network zones, air gap concepts|
|2.5-F Patching|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Update management|

### DOMAIN 3 — SECURITY ARCHITECTURE

|Requirement|Mission 03 Completion|Rationale|
|---|---|---|
|3.1-A On-premises architecture|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Primary focus of mission|
|3.1-B Cloud architecture|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Hybrid comparison|
|3.1-C Virtualization|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|VM security basics|
|3.1-D IoT architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06/M05 ownership|
|3.1-E ICS architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Verification Lab reserved|
|3.1-F Infrastructure as Code|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Automation concepts|
|3.2-A Infrastructure considerations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Network design decisions|
|3.2-B Control selection|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Security control justification|
|3.2-C Secure communication|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|TLS, encrypted channels|
|3.2-D Secure access|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM, network access|
|3.3-A Relevant data types|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M07/M08 ownership|
|3.3-B Data securing methods|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Encryption at rest/in transit|
|3.3-C Data protection|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M07/M08 ownership|
|3.3-D Data classifications|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|3.4-A High availability|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Redundancy concepts|
|3.4-B Site considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09/M02 ownership|
|3.4-C Resilience/recovery testing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Backup restoration tests|
|3.4-D Power considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09/M02 ownership|
|3.4-E Platform diversity|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09/M02/M07 ownership|
|3.4-F Backups|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Backup implementation|
|3.4-G Continuity of operations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|

### DOMAIN 4 — SECURITY OPERATIONS

|Requirement|Mission 03 Completion|Rationale|
|---|---|---|
|4.1-A Secure baselines|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Hardening standards|
|4.1-B Mobile solutions|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06/M01 ownership|
|4.1-C Hardening|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Host/network hardening|
|4.1-D Wireless security|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M02/M06 ownership|
|4.1-E Application security|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M04/M07 ownership|
|4.1-F Sandboxing|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M03/M07 ownership|
|4.1-G Monitoring computing|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|SIEM, logging|
|4.2-A Asset acquisition|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-B Asset disposal|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-C Asset assignment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-D Asset monitoring/tracking|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Inventory management|
|4.3-A Identify vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Scanning concepts|
|4.3-B Analyze vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M07 ownership|
|4.3-C Remediate vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Patching implementation|
|4.3-D Validate remediation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Post-patch scanning|
|4.3-E Report vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|4.4-A Monitoring tools|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|SIEM, IDS/IPS config|
|4.4-B Resource activities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Log analysis|
|4.5-A Firewalls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Configuration and testing|
|4.5-B IDS/IPS|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Rule creation and testing|
|4.5-C DNS filtering|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|DNS sinkhole/filtering|
|4.5-D DLP|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M05/M07/M08 partial|
|4.5-E NAC|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Port security, 802.1X concepts|
|4.5-F EDR/XDR|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M04/M05/M07 ownership|
|4.6-A Provisioning|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|User account creation|
|4.6-B SSO|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07/M05 ownership|
|4.6-C MFA|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Concept implementation|
|4.6-D Privileged access tools|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Admin account management|
|4.7-A Automation use cases|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Config automation scripts|
|4.7-B Scripting benefits|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Bash/Python examples|
|4.7-C Automation considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Reliability, testing|
|4.8-A Incident response processes|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M09 ownership|
|4.8-B Incident response training|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|
|4.8-C Incident response testing|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M09 ownership|
|4.8-D Root cause analysis|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M09 ownership|
|4.8-E Threat hunting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M07 ownership|
|4.8-F Digital forensics|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M01/M05 ownership|
|4.9-A Log data for investigations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Log collection/testing|
|4.9-B Other data sources|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Metadata, configs|

### DOMAIN 5 — SECURITY PROGRAM MANAGEMENT & OVERSIGHT

|Requirement|Mission 03 Completion|Rationale|
|---|---|---|
|5.1-A Guidelines|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Policy documentation|
|5.1-B Policies|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Security policy creation|
|5.1-C Standards|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Configuration standards|
|5.1-D Procedures|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Step-by-step documentation|
|5.1-E External considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-F Governance monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|
|5.1-G Governance structures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-H Roles/responsibilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|RACI documentation|
|5.2-A Risk identification|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Threat modeling|
|5.2-B Risk assessment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M02/M04 ownership|
|5.2-C Risk analysis|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M02/M04 ownership|
|5.2-D Risk register|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-E Risk tolerance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-F Risk appetite|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-G Risk strategies|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M07/M09 ownership|
|5.2-H Risk reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-I BIA|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.3-A Vendor assessment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-B Vendor selection|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-C Vendor agreements|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-D Vendor monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07/M08 ownership|
|5.3-E Vendor questionnaires|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-F Rules of engagement|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|5.4-A Compliance reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.4-B Non-compliance consequences|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.4-C Compliance monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M07 ownership|
|5.4-D Privacy|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M05/M07 ownership|
|5.5-A Attestation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 + Verification Lab|
|5.5-B Internal audits|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Self-assessment exercises|
|5.5-C External audits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 + Verification Lab|
|5.5-D Penetration testing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Basic scan concepts|
|5.6-A Phishing training|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.6-B Recognize anomalous behavior|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Monitoring training|
|5.6-C User guidance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M04 ownership|
|5.6-D User reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|
|5.6-E Monitoring|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Security monitoring|

---

## 12. COVERAGE INTEGRITY RESULT

The Atlas Register confirms Mission 03 fills these primary coverage gaps from Mission 01 and 02:

|Mission 01/02 Weak Area|Mission 03 Strengthens|
|---|---|
|Enterprise control depth|Firewalls, IDS/IPS, NAC implementation|
|Policy creation|Written procedures, standards, guidelines|
|Access control implementation|IAM, provisioning, RBAC|
|Change management|Documented procedures, version control|
|Security architecture|Defense-in-depth design|
|Automation|Scripting, config management|
|GNS3 hands-on execution|~90% lab compatibility|

All orphaned requirements from Mission 01/02 (![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target) remain covered elsewhere in the Atlas.

---

## 13. LABS (FREE TOOLS ONLY)

These are planned labs. Nothing is demonstrated merely because it appears here. All labs use 100% free tools.

|Lab|Objective|Tools|Security+ Links|
|---|---|---|---|
|Lab 01 — Enterprise Architecture Design|Create network topology with DMZ, internal, management zones. Document design decisions.|[draw.io](http://draw.io/), pen+paper|3.1-A, 3.2-A, 3.2-B|
|Lab 02 — Firewall Configuration|Configure stateful firewall rules for perimeter security. Test allow/deny policies.|GNS3 (pfSense/ASA), Packet Tracer|1.1-B, 2.5-B, 4.5-A|
|Lab 03 — Network Segmentation|Implement VLANs and inter-VLAN routing with access control.|GNS3/Packet Tracer switches/routers|2.5-A, 3.2-A, 1.2-H|
|Lab 04 — IDS/IPS Deployment|Configure intrusion detection rules. Generate test traffic and validate alerts.|GNS3 (Snort/Suricata), Packet Tracer|1.1-F, 4.5-B, 4.4-A|
|Lab 05 — Access Control Setup|Create user accounts, groups, and role-based permissions. Test authorization.|GNS3 virtual hosts, Linux/Windows VMs|1.2-E, 1.2-F, 4.6-A/C|
|Lab 06 — Host Hardening|Apply security baselines to workstations/servers. Document before/after configs.|GNS3 VMs, CIS benchmarks|1.1-B, 2.5-D, 4.1-A/C|
|Lab 07 — DNS Filtering|Configure DNS sinkhole/filtering. Block test domains and verify blocking.|GNS3 (Pi-hole/DNSmasq)|4.5-C, 2.2-B|
|Lab 08 — Monitoring Implementation|Deploy log collection and analyze sample events. Correlate across sources.|GNS3, Wireshark, Splunk Free|4.1-G, 4.4-A/B, 4.9-A|
|Lab 09 — Security Policy Creation|Write security policies (acceptable use, password, change management).|Word processor (free)|1.1-J, 5.1-A/B/C/D|
|Lab 10 — Change Management|Document, approve, implement, and validate a configuration change.|Version control (Git), ticket template|1.3-A/B/C/D|
|Lab 11 — Automation Scripting|Write scripts to automate security config deployment.|Bash/Python (free)|4.7-A/B/C|
|Lab 12 — Control Validation Testing|Test all implemented controls. Document effectiveness evidence.|Manual testing, vulnerability scans|2.5-A/B/C/D/E, 3.4-C|
|Lab 13 — Backup & Restore Testing|Implement backup strategy and validate restoration.|rsync, tar, GNS3 storage|3.4-F, 1.1-H|
|Lab 14 — Comprehensive Architecture Review|Document complete secure network with all controls. Present narrative.|All above artifacts|Aggregate coverage|

---

## 14. FAILURE SCENARIOS

|Scenario|Expected Behavior|Investigation Focus|
|---|---|---|
|Failure A — Firewall rule misconfiguration|Traffic blocked where allowed (or vice versa)|Rule analysis, troubleshooting|
|Failure B — VLAN leakage|Unauthorized cross-segment traffic|Segmentation validation|
|Failure C — IDS alert false positive/negative|Detection gap identified|Signature tuning|
|Failure D — Access grant too permissive|Unauthorized resource access|Permission review|
|Failure E — Patching vulnerability exposed|Unpatched system compromise|Update management process|
|Failure F — Log collection failure|Missing forensic data|Log pipeline validation|
|Failure G — Backup corruption|Unable to restore|Backup verification|
|Failure H — Policy violation detected|User non-compliance identified|Enforcement mechanism|

---

## 15. ATTACK SCENARIOS

|Attack Vector|Simulation Approach|Safety Constraints|
|---|---|---|
|Port scanning|Nmap scan from attack VM|Isolated GNS3 lab|
|Unauthorized access attempt|Failed login, privilege escalation test|Own lab only|
|VLAN hopping attempt|Tag manipulation in controlled env|Isolated GNS3 lab|
|Firewall rule bypass|Test edge cases in configs|Isolated GNS3 lab|
|DNS poisoning concept|Modified DNS response in lab|Isolated GNS3 lab|
|Brute force password test|Account lockout validation|Own accounts only|
|Malware concept testing|Safe EICAR test file|Containment required|
|Network sniffing|Wireshark on own segments|Isolated GNS3 lab|

Security Principle: All offensive simulations confined to authorized laboratory environments only (GNS3 isolated topology). No targeting of production systems.

---

## 16. TANGIBLE ARTIFACTS

Mission 03 will produce:

|Artifact|Security+ Mapping|
|---|---|
|Network architecture diagram (Level 0-2)|3.1-A, 3.2-A|
|Firewall rule set with justification|1.1-B, 4.5-A|
|VLAN configuration documentation|2.5-A, 3.2-A|
|IDS/IPS rule set and alert samples|1.1-F, 4.5-B|
|Access control matrix (users/groups/resources)|1.2-E/F/G, 4.6-A|
|Host hardening checklist (before/after)|2.5-D, 4.1-A/C|
|DNS filtering configuration|4.5-C|
|Log collection architecture|4.1-G, 4.4-A/B|
|Security policy document package|1.1-J, 5.1-A/B/C/D|
|Change management ticket template|1.3-A/B/C/D|
|Automation scripts with documentation|4.7-A/B/C|
|Control validation test results|All demonstrated|
|Backup strategy and restore proof|3.4-F, 1.1-H|
|Comprehensive architecture review|Aggregate|
|Mission 03 technical report|Aggregate|
|Security+ coverage record|All demonstrated objectives|

---

## 17. EVIDENCE OF LEARNING

Actual learner state tracked separately from planned coverage:

|Planned (Passport)|Actual (Evidence)|
|---|---|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated (design intent)|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not encountered (execution pending)|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood (design intent)|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered (limited execution)|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered (design intent)|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood (partial execution)|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated (unexpected success)|
|—|![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png) Exam verified (post-exam)|

---

## 18. SECURITY+ COVERAGE VS. LEARNER STATE

Same principle as Mission 01/02: Planned ≠ Actual.

Execution must produce evidence before awarding demonstrated status.

---

## 19. FAILURE / ATTACK / CHANGE DISCIPLINE

Same cycle as Mission 01/02:

`BASELINE → CHANGE → OBSERVE → DOCUMENT → ANALYZE → RESTORE → VALIDATE`

---

## 20. OPEN QUESTIONS

|Question|Investigation Path|
|---|---|
|What firewall rules constitute a secure baseline?|CIS benchmarks, industry standards|
|How many VLANs are appropriate for small enterprise?|Organizational size analysis|
|What IDS signatures detect common attacks?|Snort/Suricata rule libraries|
|How often should policies be reviewed?|Industry best practices|
|What constitutes adequate logging?|Retention requirements, audit needs|
|How is least privilege enforced technically?|RBAC implementation|
|What automation tools scale well for security?|Ansible, PowerShell, Bash|
|What validation proves control effectiveness?|Test methodology|
|Which Security+ objectives remain underserved?|Gap analysis|

---

## 21. CURIOSITY BRANCHES

|Branch|Notes|
|---|---|
|Advanced firewall features|Stateful inspection, application-layer filtering|
|WAF (Web Application Firewall)|Application-layer protection|
|SIEM correlation rules|Event aggregation and alerting|
|Vulnerability scanner integration|Nessus/OpenVAS concepts|
|Active Directory depth|Group policy, Kerberos|
|Container security|Docker/Kubernetes basics|
|DevSecOps concepts|CI/CD pipeline security|
|Security certifications|ISO 27001, SOC 2 overview|

---

## 22. DEFERRED TOPICS

|Topic|Reason Deferred|
|---|---|
|Deep cloud security (AWS/Azure specifics)|M07 ownership|
|Advanced cryptographic implementation|M01/M05/M07 ownership|
|Enterprise IAM complexity|M07/M08 ownership|
|Detailed compliance frameworks|M08 ownership|
|Advanced threat hunting|M04 ownership|
|Forensic investigation depth|M04 ownership|
|Industrial control systems|Verification Lab|
|Penetration testing methodology|M04 ownership|

---

## 23. PRESSURE-TEST FINDINGS

Strong coverage areas:

- Enterprise security architecture (3.2-A/B)
- Security controls implementation (1.1-A/B/E/F/H/J)
- Network security (4.5-A/B/C)
- Access control (1.2-E/F, 4.6-A)
- Hardening/baselines (2.5-D, 4.1-A/C)
- Policy creation (5.1-A/B/C/D)
- Change management (1.3-A/B/C/D)
- Automation (4.7-A/B)
- GNS3/Packet Tracer compatibility (~90%)

Natural crossover with Mission 01 (networking) and Mission 02 (availability) provides reinforcement without duplication.

---

## 24. WHAT THE PRESSURE TEST REJECTED

Mission 03 will not artificially expand to demonstrate:

- Deep cloud architecture (M07)
- Satellite/LEO security (M02)
- Incident response lifecycle (M04)
- AI application security (M05)
- Drone/mobile operational security (M06)
- Third-party/vendor risk (M08)
- Business continuity (M09)
- Blockchain (Verification Lab)
- ICS architecture (Verification Lab)
- Full IAM/SSO implementation (M07)

---

## 25. NEXT MISSION CONNECTIONS

|Future Mission|Connection Points|
|---|---|
|Mission 04 — Network Compromised|Applies M03 controls to incident investigation|
|Mission 05 — Secure AI Capability|Extends application security beyond M03 basics|
|Mission 06 — Drone ISR|Physical/mobile security extension of M03|
|Mission 07 — Move to Cloud|Cloud transformation of M03 architecture|
|Mission 08 — System Nobody Understands|Governance layer over M03 controls|
|Mission 09 — Everything Is Failing|Resilience integration across all architectures|

Mission 03 establishes foundational security controls that later missions assume.

---

## 26. CURRENT STATE

|Item|Status|
|---|---|
|Mission status|Not started|
|Architecture|Defined at conceptual level|
|Security+ coverage design|Aligned with Atlas|
|Atomic requirements|All accounted|
|Planned completion coverage|Defined|
|Labs|Designed, not executed|
|Artifacts|None produced yet|
|Security+ evidence|None yet|
|Learner state|Not pre-awarded|
|Lab cost|$0 (all free tools)|

---

## 27. WHAT WE KNOW

At mission launch, we know the intended architecture and learning objectives. We do not assume paper architecture equals demonstrated knowledge.

---

## 28. WHAT WE HAVE BUILT

Architecture and learning design complete. Laboratory implementation pending. First artifact will be network architecture diagram.

---

## 29. NEXT RECOMMENDED ACTION

Begin with Level 0 → Level 1 architecture design. First question:

"What security zones does an enterprise network need, and how do they connect?"

That question determines the first conceptual branch.

---

## 30. MISSION COMPLETE WHEN

Mission 03 is complete only when:

- Architecture diagrams produced
- Network journey explained end-to-end
- Protocols and controls configured
- Firewall/IDS/IPS tested
- Failure scenarios tested
- Security policies documented
- Change management exercised
- Automation scripts created
- Backup/restore validated
- Control effectiveness proven
- Tangible artifacts assembled
- Security+ evidence recorded
- Remaining gaps identified
- Uncovered objectives assigned to later missions or Verification Labs

---

## 31. HANDOFF NOTES FOR ANOTHER AI

Do not restart this mission from scratch. The learner uses a systems-journey learning model. Destination is CompTIA Security+ V7.

Key reminders:

- Do not turn this into a networking course
- Focus on Security+ objectives, not certification for vendors
- Require evidence before awarding demonstrated status
- Preserve coverage integrity per Atlas Register
- Use Verification Labs for orphaned objectives (Blockchain, ICS, attestation)
- Maintain all labs at $0 cost (GNS3, Packet Tracer, free tools only)
- Keep offensive activities isolated to own lab

Governing principle: Security+ is the destination. The Mission Atlas is the vehicle.

---

## 32. ARCHITECTURAL FREEZE

Incorporating Atlas Register frozen principles:

|Principle|Applied to Mission 03|
|---|---|
|Every Security+ requirement represented in Atlas|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Coverage table maps all|
|Passport uses atomic Security+ coverage|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Table uses 1.1-A through 5.6-E|
|Coverage = intended completion, not current|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Distinction maintained|
|Four planning classes (![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png))|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Applied throughout|
|Five-state learner vocabulary (![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png))|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Separate from planned|
|Mission ownership ≠ Atlas coverage|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Reinforcement tracked|
|No artificial expansion|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Rejected items listed|
|Verification Labs for gaps|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Blockchain, ICS reserved|
|4.8 IR + 4.9 Data Sources separate|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Maintained in coverage table|
|Labs planned until executed|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) All labs marked planned|
|Artifacts not produced until existing|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Zero artifacts currently|
|Labs must be 100% free|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) All labs use free tools only|