# MISSION PASSPORT

# MISSION: 04 — The Network Is Compromised

## VERSION: 1.0 — Architecture Draft

## STATUS: Designed / Not Executed

## DESTINATION: CompTIA Security+ V7

---

## 1. DESTINATION

CompTIA Security+ V7

Mission 04 is designed to demonstrate specific Security+ objectives through incident response, threat analysis, and digital forensics. All atomic requirements are accounted for in the Atlas Register. This Passport must align with the master coverage map.

Cost Constraint: All labs executable with 100% free tools (GNS3, Packet Tracer, Wireshark, Autopsy, Volatility, Splunk Free, open-source malware sandboxes).

---

## 2. MISSION INTENT

Understand how to investigate, contain, and recover from a security incident within an enterprise network.

The mission begins with this critical question:

"How do we know we are breached, and what do we do when we find out?"

The objective is to develop the ability to:

|Skill|Purpose|
|---|---|
|Detect security anomalies|Distinguish noise from threats|
|Perform triage and initial assessment|Determine severity quickly|
|Preserve digital evidence|Maintain chain of custody|
|Analyze malicious activity|Identify malware/attack vectors|
|Conduct root cause analysis|Find the entry point|
|Execute containment strategies|Stop lateral movement|
|Lead eradication and recovery|Restore secure operations|
|Document lessons learned|Improve future posture|
|Map demonstrated knowledge to Security+|Produce exam-ready evidence|
|Produce tangible evidence of learning|Portfolio artifacts|

Security+ concepts will be introduced when they become necessary to answer questions about the incident lifecycle.

---

## 3. SCENARIO

An enterprise organization (from Mission 03) detects anomalous behavior.

Possible indicators:

- Unexpected outbound traffic spikes
- New user accounts in Active Directory
- Antivirus alerts ignored
- Unusual login times/locations
- File encryption attempts detected

The mission is to act as the security team responding to this event:

`DETECTION SIGNAL ↓ INITIAL TRiage ↓ EVIDENCE PRESERVATION ↓ INVESTIGATION (Logs, Memory, Disk) ↓ CONTAINMENT (Network isolation, account disable) ↓ ERADICATION (Malware removal, patching) ↓ RECOVERY (Restoration, monitoring) ↓ POST-INCIDENT REVIEW (Reporting, Lessons Learned)`

This contrasts with Mission 01 (normal operation), 02 (infrastructure analysis), and 03 (building secure controls) by focusing on breaking and fixing a system under attack.

---

## 4. END STATE

Mission 04 is complete when the learner can independently:

|Competency|Evidence Required|
|---|---|
|Identify signs of compromise|Anomaly detection report|
|Classify incident severity|Severity assessment document|
|Preserve evidence legally|Chain of custody forms, hash logs|
|Analyze network traffic|Wireshark PCAP analysis report|
|Examine host artifacts|Memory/Disk forensic reports|
|Trace attack kill chain|Timeline reconstruction|
|Implement containment actions|Firewall/ACL change logs|
|Remove persistent threats|Malware removal evidence|
|Verify system recovery|Clean scan results|
|Write incident report|Executive summary + technical details|
|Map demonstrated knowledge to Security+|Coverage matrix update|
|Produce tangible evidence of learning|Portfolio artifacts|
|Explain the incident coherently|Narrative without script|

---

## 5. WHY THIS MISSION EXISTS

This mission serves specific purposes that Mission 01, 02, and 03 do not cover:

|Purpose|How Mission 04 Delivers|
|---|---|
|Incident Response Lifecycle|Prep, Detect, Contain, Eradicate, Recover, Lessons|
|Digital Forensics|Memory, disk, network evidence analysis|
|Threat Intelligence|Understanding actors, TTPs, IOCs|
|Log Analysis|Correlating data sources (4.9)|
|Malware Analysis|Static/dynamic analysis basics|
|Root Cause Analysis|Going beyond symptoms|
|Post-Incident Governance|Reporting, policy updates|
|GNS3/Packet Tracer Compatibility|~85% executable with free tools + VMs|

Security+ Domain 4.8 (Incident Response), 4.9 (Data Sources), and Domain 2 (Threats/Vulnerabilities/Malicious Activity) all receive primary treatment here.

---

## 6. SYSTEM ARCHITECTURE

Exploration occurs across multiple zoom levels:

### LEVEL 0 — Business Impact View

`ATTACK DETECTED ↓ BUSINESS STOPPED? ↓ DATA STEAL? ↓ FINANCIAL LOSS?`

### LEVEL 1 — Incident Response View

`PREPARATION ↓ IDENTIFICATION ↓ CONTAINMENT ↓ ERADICATION ↓ RECOVERY ↓ LESSONS LEARNED`

### LEVEL 2 — Technical Investigation View

`┌─────────────────────────────────────────────────────────┐ │ DATA SOURCES │ │ • Network Logs (Firewall, IDS, DNS, Proxy) │ │ • Host Logs (OS, Event Viewer, Syslog) │ │ • Application Logs (Web Server, DB, App) │ │ • Endpoint Data (RAM, Disk, Registry) │ │ • Threat Intel Feeds (IOCs) │ ├─────────────────────────────────────────────────────────┤ │ ANALYSIS TOOLS │ │ • Wireshark (Traffic) │ │ • Splunk/ELK (Log Correlation) │ │ • Volatility (Memory Forensics) │ │ • Autopsy (Disk Forensics) │ │ • FLARE-VM (Malware Analysis) │ └─────────────────────────────────────────────────────────┘`

### LEVEL 3 — Kill Chain View

`RECONNAISSANCE → DELIVERY → EXPLOITATION → INSTALLATION → C2 → ACTIONS`

### LEVEL 4 — Evidence Collection View

`Volatile Data (RAM, Processes) ↓ Network Traffic (PCAP) ↓ System Logs (Event Logs, Syslog) ↓ Disk Images (Bit-by-bit copies) ↓ Artifacts (Prefetch, JumpLists, Browser History)`

### LEVEL 5 — Evidence Validity View

|Evidence Type|Integrity Method|Chain of Custody Need|
|---|---|---|
|PCAP Files|SHA-256 Hash|Yes (Critical)|
|RAM Dump|Hash|Yes (Critical)|
|Logs|WORM Storage|Yes (High)|
|Screenshots|Timestamp/Hash|Yes (Medium)|
|Interviews|Recorded/Notarized|Yes (Legal)|

---

## 7. SYSTEM JOURNEY

The canonical journey for this mission:

`NORMAL OPERATIONS ↓ ANOMALY DETECTION (Alert, User Report, Scan) ↓ INITIAL TRIAGE (Severity, Scope, Urgency) ↓ EVIDENCE ACQUISITION (Preserve State) ↓ INVESTIGATION PHASE (Logs, Forensics, Hunt) ↓ THREAT CLASSIFICATION (Malware, Insider, APT) ↓ CONTAINMENT STRATEGY (Network, Host, Account) ↓ ERADICATION (Remove Rootkit, Patch, Reset) ↓ RECOVERY PLAN (Restore, Validate, Monitor) ↓ REPORTING (Executive, Technical, Regulatory) ↓ IMPROVEMENT (Update Policies, Tools) ↓ SECURITY+ COVERAGE RECORD`

This decomposition becomes the investigation framework.

---

## 8. CORE QUESTIONS

### Detection

- How do we distinguish false positives from real threats?
- What logs indicate a breach early?
- Who gets notified first?
- What constitutes "enough evidence" to declare an incident?

### Evidence

- How do we capture volatile data before it vanishes?
- How do we ensure evidence admissibility?
- What hashing proves integrity?
- How long do we retain logs?
- Where is the evidence stored securely?

### Analysis

- What does the traffic look like during C2 communication?
- How do we identify the initial entry point?
- What registry keys indicate persistence?
- How do we analyze a suspicious file safely?
- Can we attribute the attack to a specific actor?

### Response

- How do we isolate the affected system?
- Do we shut down or keep running (live forensics)?
- How do we reset credentials securely?
- How do we verify the threat is gone?
- Who approves system restoration?

### Recovery

- How do we rebuild without reintroducing the threat?
- How do we monitor for reinfection?
- What communications go to leadership?
- What lessons change policy?

### Legal/Compliance

- Do we notify customers? Regulators? Insurance?
- When do we involve law enforcement?
- What are the privacy implications of monitoring employees?

---

## 9. MISSION OPERATING MODEL

Mission 04 follows this cycle:

`ALERT ↓ TRIAGE ↓ PRESERVE ↓ INVESTIGATE ↓ ANALYZE ↓ CONTAIN ↓ ERADICATE ↓ RECOVER ↓ DOCUMENT ↓ IMPROVE ↓ SECURITY+ MAPPING`

Mission 04 differs from Mission 01-03 by emphasizing:

- Reaction over prevention (Responding to failure vs. building controls)
- Analysis over construction (Reading evidence vs. configuring firewalls)
- Uncertainty management (Working with incomplete data)
- Chain of Custody (Legal defensibility)

---

## 10. SECURITY+ COVERAGE MODEL

Coverage rule (per Atlas): Every Security+ atomic requirement must appear in the Atlas. Mission 04 does not need to own every requirement—it needs to account for each and define its expected contribution.

Coverage status represents expected completion coverage, not learner achievement.

### Status Vocabulary (Mission 04 Completion)

|Status|Meaning|
|---|---|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|Practical evidence expected from Mission 04|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|Explanation/application evidence, less implementation|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|Contextual understanding; deeper ownership elsewhere|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 04 Target|Accounted in Atlas; deliberately not owned here|

---

## 11. SECURITY+ ATOMIC COVERAGE TABLE

### DOMAIN 1 — GENERAL SECURITY CONCEPTS

|Requirement|Mission 04 Completion|Rationale|
|---|---|---|
|1.1-A Technical controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IR tools, forensic tools|
|1.1-B Preventive controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|1.1-C Managerial controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|IR Plans, policies|
|1.1-D Deterrent controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|1.1-E Operational controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IR procedures, response ops|
|1.1-F Detective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Alerts, monitoring, hunting|
|1.1-G Physical controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M02/M06 ownership|
|1.1-H Corrective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Recovery, patching, restore|
|1.1-I Compensating controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M09 ownership|
|1.1-J Directive controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|1.2-A Confidentiality|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Data exposure analysis|
|1.2-B Integrity|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Tampered evidence analysis|
|1.2-C Availability|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Ransomware recovery focus|
|1.2-D Non-repudiation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Log integrity, signing|
|1.2-E Authentication|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M07 ownership|
|1.2-F Authorization|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M07 ownership|
|1.2-G Accounting|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Log tracking|
|1.2-H Zero Trust|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M07 ownership|
|1.2-I Deception/disruption|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Honeypots (conceptual)|
|1.3-A Change mgmt processes|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Emergency change process|
|1.3-B Technical implications|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|1.3-C Change documentation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|1.3-D Version control|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M07 ownership|
|1.4-A PKI|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M05/M06/M07 ownership|
|1.4-B Encryption|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M03/M05/M06/M07 ownership|
|1.4-C Obfuscation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Malware techniques|
|1.4-D Hashing|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Evidence integrity verification|
|1.4-E Digital signatures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M05/M06/M07 ownership|
|1.4-F Blockchain|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target|Verification Lab reserved|

### DOMAIN 2 — THREATS, VULNERABILITIES & MITIGATIONS

|Requirement|Mission 04 Completion|Rationale|
|---|---|---|
|2.1-A Nation-state actors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|APT analysis concepts|
|2.1-B Unskilled attackers|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Script kiddie tools|
|2.1-C Hacktivists|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Motivation analysis|
|2.1-D Insider threats|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Privilege abuse detection|
|2.1-E Organized crime|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Ransomware gangs|
|2.1-F Shadow IT|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|2.1-G Data exfiltration|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Network traffic analysis|
|2.1-H Espionage motivation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|APT context|
|2.1-I Financial gain motivation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Ransomware focus|
|2.2-A Message-based vectors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Phishing attachment analysis|
|2.2-B Unsecure network vectors|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Lateral movement analysis|
|2.2-C Social engineering vectors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Spear-phishing analysis|
|2.2-D File-based vectors|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Malware sample analysis|
|2.2-E Voice call vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M06/M08 partial|
|2.2-F Supply chain vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M08 ownership|
|2.2-G Vulnerable software vectors|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Exploit analysis|
|2.2-H Attack surfaces|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Exposure identification|
|2.3-A Application vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M07 ownership|
|2.3-B Hardware vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M02/M06 ownership|
|2.3-C Mobile device vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06 ownership|
|2.3-D Virtualization vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|2.3-E OS-based vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Exploitation analysis|
|2.3-F Cloud-specific vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|2.3-G Web-based vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|2.3-H Supply chain vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M08 ownership|
|2.4-A Malware attacks|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Analysis of samples|
|2.4-B Password attacks|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cracking hash samples|
|2.4-C Application attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|2.4-D Physical attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M02/M06 ownership|
|2.4-E Network attacks|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Mitm, sniffing, DoS analysis|
|2.4-F Cryptographic attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M05 ownership|
|2.5-A Segmentation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Lateral movement containment|
|2.5-B Access control|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Account lockout/reset|
|2.5-C Configuration enforcement|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|2.5-D Hardening|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|2.5-E Isolation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Quarantine procedures|
|2.5-F Patching|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Post-incident patching|

### DOMAIN 3 — SECURITY ARCHITECTURE

|Requirement|Mission 03 Completion|Rationale|
|---|---|---|
|3.1-A On-premises architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|3.1-B Cloud architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|3.1-C Virtualization architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|3.1-D IoT architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06 ownership|
|3.1-E ICS architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Verification Lab reserved|
|3.1-F Infrastructure as Code|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|3.2-A Infrastructure considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|3.2-B Control selection|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|3.2-C Secure communication|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|3.2-D Secure access|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|3.3-A Relevant data types|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M08 ownership|
|3.3-B Data securing methods|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M07 ownership|
|3.3-C Data protection considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M07/M08 ownership|
|3.3-D Data classifications|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|3.4-A High availability|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09 ownership|
|3.4-B Site considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09 ownership|
|3.4-C Resilience/recovery testing|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|DR testing post-incident|
|3.4-D Power considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09 ownership|
|3.4-E Platform diversity|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M09 ownership|
|3.4-F Backups|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Restoration verification|
|3.4-G Continuity of operations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|BCP activation|

### DOMAIN 4 — SECURITY OPERATIONS

|Requirement|Mission 04 Completion|Rationale|
|---|---|---|
|4.1-A Secure baselines|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|4.1-B Mobile solutions|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06 ownership|
|4.1-C Hardening|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|4.1-D Wireless security|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M02/M06 ownership|
|4.1-E Application security|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|4.1-F Sandboxing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Malware analysis concepts|
|4.1-G Monitoring computing resources|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Active monitoring during IR|
|4.2-A Asset management|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-B Asset disposal|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-C Asset assignment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-D Asset monitoring/tracking|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Asset inventory for IR|
|4.3-A Identify vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Post-breach scanning|
|4.3-B Analyze vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Exploit linkage|
|4.3-C Remediate vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Patching as mitigation|
|4.3-D Validate remediation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Rescan post-patch|
|4.3-E Report vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IR reporting|
|4.4-A Alerting and Monitoring|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|SIEM analysis, alert triage|
|4.4-B Computing resource activities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Log correlation|
|4.5-A Firewalls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Blocking attacker IPs|
|4.5-B IDS/IPS|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Alert tuning during IR|
|4.5-C DNS filtering|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Sinkholing malicious domains|
|4.5-D DLP|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M05/M07/M08 ownership|
|4.5-E NAC|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M07 ownership|
|4.5-F EDR/XDR|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|EDR log analysis|
|4.6-A Provisioning|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|4.6-B SSO|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|4.6-C MFA|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|4.6-D Privileged access tools|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07 ownership|
|4.7-A Automation and Orchestration|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|SOAR concepts|
|4.7-B Scripting benefits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M05/M07 ownership|
|4.7-C Automation considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M05/M07 ownership|
|4.8-A Incident response processes|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|NIST/SANS lifecycle applied|
|4.8-B Incident response training|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Tabletop exercises|
|4.8-C Incident response testing|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IR drill execution|
|4.8-D Root cause analysis|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Fishbone/5 Whys applied|
|4.8-E Threat hunting|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Proactive search for IOCs|
|4.8-F Digital forensics|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Memory/Disk/Network forensics|
|4.9-A Use log data to support investigations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|SIEM/Log analysis|
|4.9-B Use other data sources to support investigations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Memory dumps, PCAP, artifacts|

### DOMAIN 5 — SECURITY PROGRAM MANAGEMENT & OVERSIGHT

|Requirement|Mission 04 Completion|Rationale|
|---|---|---|
|5.1-A Guidelines|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-B Policies|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-C Standards|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-D Procedures|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|IR Playbooks|
|5.1-E External considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Regulatory notification|
|5.1-F Monitoring within governance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-G Governance structures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-H Roles/responsibilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|IR Team roles|
|5.2-A Risk identification|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.2-B Risk assessment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.2-C Risk analysis|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.2-D Risk register|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-E Risk tolerance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-F Risk appetite|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-G Risk strategies|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M07/M09 ownership|
|5.2-H Risk reporting|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Incident reporting|
|5.2-I BIA|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.3-A Vendor assessment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-B Vendor selection|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-C Vendor agreements|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-D Vendor monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M07/M08 ownership|
|5.3-E Vendor questionnaires|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-F Rules of engagement|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|IR authority definition|
|5.4-A Compliance reporting|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Breach notification laws|
|5.4-B Consequences of non-compliance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.4-C Compliance monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.4-D Privacy considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Employee monitoring|
|5.5-A Attestation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 + Verification Lab|
|5.5-B Internal audits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.5-C External audits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 + Verification Lab|
|5.5-D Penetration testing|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M05/M07 ownership|
|5.6-A Phishing training|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.6-B Recognize anomalous behavior|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Training staff to report|
|5.6-C User guidance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M04 partial|
|5.6-D User reporting|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Incident reporting channels|
|5.6-E Monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|

---

## 12. COVERAGE INTEGRITY RESULT

The Atlas Register confirms Mission 04 fills these primary coverage gaps from Mission 01-03:

|Mission 01/02/03 Weak Area|Mission 04 Strengthens|
|---|---|
|Incident Response Lifecycle|4.8-A through 4.8-F Primary|
|Digital Forensics|4.8-F, 4.9-A/B Primary|
|Threat Actor Analysis|Domain 2 Primary|
|Root Cause Analysis|4.8-D Primary|
|Evidence Handling|Chain of Custody skills|
|Log Correlation|4.9-A/B Primary|

All orphaned requirements from Mission 01-03 (![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target) remain covered elsewhere in the Atlas.

---

## 13. LABS (FREE TOOLS ONLY)

These are planned labs. Nothing is demonstrated merely because it appears here. All labs use 100% free tools.

|Lab|Objective|Tools|Security+ Links|
|---|---|---|---|
|Lab 01 — IR Plan Development|Create IR playbook (preparation, detection, containment steps).|Word Processor (Free)|4.8-A, 5.1-D|
|Lab 02 — Log Analysis|Ingest logs into Splunk Free/ELK. Write queries for anomalies.|Splunk Free, ELK Stack|4.4-A, 4.9-A|
|Lab 03 — Network Forensics|Capture PCAP. Identify malicious traffic patterns (C2, exfil).|Wireshark, TShark|4.9-B, 2.2-B, 2.4-E|
|Lab 04 — Memory Forensics|Analyze RAM dump for malware artifacts, processes, injected code.|Volatility Framework|4.8-F, 2.4-A|
|Lab 05 — Disk Forensics|Analyze disk image for deleted files, registry keys, timeline.|Autopsy, Sleuth Kit|4.8-F, 2.4-A|
|Lab 06 — Malware Analysis (Static)|Analyze binary hashes, strings, imports without executing.|FLARE-VM (Free), VirusTotal (Free)|2.4-A, 4.1-F|
|Lab 07 — Malware Analysis (Dynamic)|Execute malware in sandbox, observe behavior.|Any.Run (Free Tier), Joe Sandbox (Free)|2.4-A, 4.1-F|
|Lab 08 — Containment Simulation|Simulate isolation via firewall rules, VLAN moves in GNS3.|GNS3, Packet Tracer|2.5-E, 4.5-A|
|Lab 09 — Threat Hunting|Proactively search logs for IOCs (hashes, IPs).|Splunk Free, ThreatIntel Feeds|4.8-E, 4.9-A|
|Lab 10 — Vulnerability Lifecycle (IR Context)|Identify exploit used, patch, validate fix.|OpenVAS/Nessus Essentials (Free)|4.3-A/B/C/D/E|
|Lab 11 — Chain of Custody Exercise|Document evidence handling from collection to storage.|Forms (Free Template)|4.8-F, 1.2-D|
|Lab 12 — Root Cause Analysis|Apply 5 Whys/Fishbone to simulated incident.|Diagramming Tool|4.8-D|
|Lab 13 — IR Drill / Tabletop|Walkthrough scenario with decision tree.|Scenario Doc, Timer|4.8-C, 4.8-B|
|Lab 14 — Post-Incident Report|Write executive and technical findings.|Word Processor (Free)|4.3-E, 5.2-H|

---

## 14. FAILURE SCENARIOS

|Scenario|Expected Behavior|Investigation Focus|
|---|---|---|
|Failure A — False Positive Alert|Legitimate traffic flagged|Tuning detection rules|
|Failure B — Evidence Lost|Log rotation overwrote data|Log retention review|
|Failure C — Containment Failed|Attacker moved laterally|Segmentation review|
|Failure D — Malware Persistence|Regkey missed, infection returns|Thoroughness of eradication|
|Failure E — Communication Breakdown|Stakeholders uninformed|Reporting chain check|
|Failure F — Chain of Custody Broken|Evidence inadmissible|Documentation audit|

---

## 15. ATTACK SCENARIOS

|Attack Vector|Simulation Approach|Safety Constraints|
|---|---|---|
|Ransomware simulation|Safe EICAR file or controlled sample|Isolated VM (FLARE-VM)|
|Brute force attempt|Hashcat/John on known weak hashes|Offline cracking only|
|SQL Injection|OWASP Juice Shop container|Local container only|
|Phishing attachment|Safe macro-enabled doc|Isolated VM, no macros enabled initially|
|Network Sniffing|Wireshark capture on attack segment|Isolated GNS3 lab|
|Privilege Escalation|Known local exploit (Metasploit)|Isolated lab only|

Security Principle: All offensive simulations confined to authorized laboratory environments only. No targeting of production systems. No live malware downloaded from internet without isolation.

---

## 16. TANGIBLE ARTIFACTS

Mission 04 will produce:

|Artifact|Security+ Mapping|
|---|---|
|Incident Response Playbook|4.8-A, 5.1-D|
|Log Analysis Query Set|4.4-A, 4.9-A|
|Network Forensics Report (PCAP)|4.9-B, 2.4-E|
|Memory Forensics Report|4.8-F, 2.4-A|
|Disk Forensics Report|4.8-F, 2.4-A|
|Malware Analysis Report (Static/Dynamic)|2.4-A, 4.1-F|
|Containment Action Log|2.5-E, 4.5-A|
|Threat Hunting Results|4.8-E|
|Vulnerability Remediation Report|4.3-A/B/C/D/E|
|Chain of Custody Form|4.8-F, 1.2-D|
|Root Cause Analysis Document|4.8-D|
|IR Drill Report|4.8-B/C|
|Post-Incident Report|4.3-E, 5.2-H|
|Mission 04 Technical Report|Aggregate|
|Security+ Coverage Record|All demonstrated objectives|

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

Same principle as Mission 01-03: Planned ≠ Actual.

Execution must produce evidence before awarding demonstrated status.

---

## 19. FAILURE / ATTACK / CHANGE DISCIPLINE

Same cycle as Mission 01-03:

`BASELINE → CHANGE → OBSERVE → DOCUMENT → ANALYZE → RESTORE → VALIDATE`

Plus IR specific:

`DETECT → PRESERVE → INVESTIGATE → CONTAIN → ERADICATE → RECOVER → REPORT`

---

## 20. OPEN QUESTIONS

|Question|Investigation Path|
|---|---|
|What logs are essential for forensics?|Audit policies, log retention|
|How do we differentiate noise from threat?|Baseline traffic, threshold tuning|
|What evidence holds up in court?|Chain of custody standards|
|How do we analyze malware safely?|Isolated VMs, snapshots|
|What constitutes successful containment?|No further lateral movement|
|How do we communicate during an incident?|Reporting hierarchies|
|What legal obligations exist post-breach?|GDPR, CCPA, HIPAA basics|
|Which Security+ objectives remain underserved?|Gap analysis|

---

## 21. CURIOSITY BRANCHES

|Branch|Notes|
|---|---|
|Advanced Malware Reverse Engineering|Assembly, unpacking (optional)|
|Cloud Forensics|AWS/Azure logging (M07 tie-in)|
|Threat Intel Sharing Platforms|ISACs, MISP|
|Legal Discovery Processes|eDiscovery, subpoenas|
|Red Teaming vs. Blue Teaming|Offensive/Defensive roles|
|SOC Operations|Tier 1/2/3 analyst paths|

---

## 22. DEFERRED TOPICS

|Topic|Reason Deferred|
|---|---|
|Deep Law Enforcement Interaction|Beyond Security+ scope|
|Advanced Reverse Engineering|Specialized skill outside exam|
|Corporate Crisis Communication|M08 Governance territory|
|Insurance Claim Processing|Business continuity focus|
|Deep Threat Intel Automation|M05/M07 Automation territory|
|Advanced Encryption Breaking|M01/M05 Territory|

---

## 23. PRESSURE-TEST FINDINGS

Strong coverage areas:

- Incident Response Lifecycle (4.8-A/B/C/D/E/F)
- Digital Forensics (4.8-F)
- Data Sources for Investigation (4.9-A/B)
- Threat Analysis (Domain 2)
- Root Cause Analysis (4.8-D)
- GNS3/VM Toolchain Compatibility (~85%)

Natural crossover with Mission 03 (Controls) provides context for what failed, allowing deeper investigation of how it failed.

---

## 24. WHAT THE PRESSURE TEST REJECTED

Mission 04 will not artificially expand to demonstrate:

- Enterprise Security Architecture (M03)
- Cloud Migration (M07)
- Governance/Risk Management Depth (M08)
- Application Security Development (M05)
- Physical Satellite Security (M02)
- Business Continuity Planning (M09)
- Blockchain (Verification Lab)
- ICS Architecture (Verification Lab)

---

## 25. NEXT MISSION CONNECTIONS

|Future Mission|Connection Points|
|---|---|
|Mission 05 — Secure AI Capability|Extends malware analysis to AI models|
|Mission 06 — Drone ISR|Physical/mobile incident response|
|Mission 07 — Move to Cloud|Cloud-native incident response|
|Mission 08 — System Nobody Understands|Governance oversight of IR program|
|Mission 09 — Everything Is Failing|Integrated disaster recovery|

Mission 04 establishes investigative rigor that later missions apply to specific domains.

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

Architecture and learning design complete. Laboratory implementation pending. First artifact will be IR Playbook.

---

## 29. NEXT RECOMMENDED ACTION

Begin with Level 0 → Level 1 IR Plan Design. First question:

"What steps must occur from the moment an alert fires until the incident is closed?"

That question determines the first conceptual branch.

---

## 30. MISSION COMPLETE WHEN

Mission 04 is complete only when:

- IR Playbook created
- Logs analyzed
- Forensics performed (Memory/Disk/Network)
- Malware analyzed (Safe)
- Containment practiced
- Vulnerabilities patched post-incident
- Root Cause documented
- Chain of Custody maintained
- Post-Incident Report written
- Tangible artifacts assembled
- Security+ evidence recorded
- Remaining gaps identified
- Uncovered objectives assigned to later missions or Verification Labs

---

## 31. HANDOFF NOTES FOR ANOTHER AI

Do not restart this mission from scratch. The learner uses a systems-journey learning model. Destination is CompTIA Security+ V7.

Key reminders:

- Do not turn this into a cybercrime course
- Focus on Security+ objectives, not certification for vendors
- Require evidence before awarding demonstrated status
- Preserve coverage integrity per Atlas Register
- Use Verification Labs for orphaned objectives (Blockchain, ICS, attestation)
- Maintain all labs at $0 cost (GNS3, Splunk Free, Volatility, Autopsy)
- Keep offensive activities isolated to own lab
- Emphasize safety (isolated VMs) for malware analysis

Governing principle: Security+ is the destination. The Mission Atlas is the vehicle.

---

## 32. ARCHITECTURAL FREEZE

Incorporating Atlas Register frozen principles:

|Principle|Applied to Mission 04|
|---|---|
|Every Security+ requirement represented in Atlas|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Coverage table maps all|
|Passport uses atomic Security+ coverage|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Table uses 1.1-A through 5.6-E|
|Coverage = intended completion, not current|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Distinction maintained|
|Four planning classes (![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png))|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Applied throughout|
|Five-state learner vocabulary (![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png))|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Separate from planned|
|Mission ownership ≠ Atlas coverage|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Reinforcement tracked|
|No artificial expansion|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Rejected items listed|
|Verification Labs for gaps|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Blockchain, ICS reserved|
|4.8 IR + 4.9 Data Sources separate|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Maintained in coverage table (Primary M04)|
|Labs planned until executed|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) All labs marked planned|
|Artifacts not produced until existing|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Zero artifacts currently|
|Labs must be 100% free|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) All labs use free tools only|