
# LAB 11 — INCIDENT RECONSTRUCTION

## Objective

Given only evidence (no prior knowledge of what happened), reconstruct what occurred during a simulated security event. Produce a timeline, identify affected components, determine root cause, document supporting evidence, specify involved security controls, and recommend remediation.

This simulates an actual **forensic investigation scenario** where you must piece together what happened from scattered evidence.

---

## Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.8-A|Implement incident response processes|🟡 Understood|IR methodology applied systematically|
|4.8-C|Conduct incident response testing|🟢 Demonstrated|Controlled incident scenario executed|
|4.8-D|Perform root cause analysis|🟢 Demonstrated|Root cause identified through systematic analysis|
|4.8-E|Conduct threat hunting|🟡 Understood|Hypothesis-driven evidence gathering|
|4.8-F|Conduct/use digital forensics|🟢 Demonstrated|Chain-of-custody preserved, evidence analyzed|
|4.9-A|Use log data for investigations|🟢 Demonstrated|Multiple log sources correlated|
|4.9-B|Use other data sources for investigations|🟢 Demonstrated|Packet capture, endpoint data used|
|2.4-E|Network attacks|🟢 Demonstrated|Attack pattern reconstructed|
|1.3-C|Change documentation|🟡 Understood|Investigation findings documented|

---

## Prerequisites

- Labs 07–10 complete (firewall rules, vulnerability lifecycle, monitoring)
- Ubuntu Server VM still running with Apache + Suricata
- Familiarity with Wireshark, Apache logs, auth.log, packet captures

---

## Tools

- Wireshark
- Ubuntu Server VM (from Labs 09–10)
- Text editor / markdown for report
- draw.io (for timeline diagram)
- Python 3 (optional, for log parsing)
- `sha256sum` or `md5sum` (for evidence hashing)

---

## Environment Setup

### Important: Separation of Roles

This lab requires two perspectives:

1. **Attacker** (creates the incident)
2. **Investigator** (reconstructs what happened)

Ideally, these should be done at different times or by different people. Since you're doing this alone, create the incident scenario first, then **hide your notes** before investigating.

---

### Part A — Set Up the Crime Scene (Do First)

**Run this attack sequence from a separate terminal or another VM:**

`# ATTACKER MACHINE (could be your host or a second VM) TARGET_IP="<your-ubuntu-vm-ip>" # Step 1: Port reconnaissance nmap -sS "$TARGET_IP" # Step 2: Service enumeration nmap -sV -p 80,443,22,3306 "$TARGET_IP" # Step 3: Web application probing curl -A "Mozilla/5.0" "http://$TARGET_IP/robots.txt" curl "http://$TARGET_IP/.git/config" 2>/dev/null curl "http://$TARGET_IP/.env" 2>/dev/null # Step 4: SSH brute-force attempt (with invalid credentials) hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://"$TARGET_IP" || true # Step 5: Create a suspicious file (simulating compromise artifact) ssh admin@"$TARGET_IP" <<EOF echo "EXFILTRATED_DATA_TEST" > /tmp/suspicious_file.txt touch -t 202608141200 /tmp/suspicious_file.txt EOF`

### Preserve Evidence

**On the target VM:**

`# Create evidence directory mkdir -p ~/evidence/incident # Copy all relevant logs cp /var/log/apache2/access.log ~/evidence/incident/apache_access.log.bak cp /var/log/apache2/error.log ~/evidence/incident/apache_error.log.bak cp /var/log/auth.log ~/evidence/incident/auth.log.bak cp /var/log/suricata/fast.log ~/evidence/incident/suricata_alerts.log.bak # Capture a new packet trace during the attack window sudo tcpdump -i enp0s3 -w ~/evidence/incident/incident_capture.pcap & TCPDUMP_PID=$! # Wait a moment, then stop sleep 30 kill $TCPDUMP_PID # Hash all evidence files for integrity verification cd ~/evidence/incident sha256sum *.log.bak *.pcap > checksums.txt`

**Now hide your attack notes:**

Move or rename any documents you created describing what you did. The investigator (you in Phase B) should **not know** what happened.

---

### Part B — Begin the Investigation

You now have access to:

- The `~/evidence/incident/` directory with logs and packet capture
- The target VM (read-only access to evidence)
- **No prior knowledge** of what occurred

---

## Procedure

### Step 1 — Secure and Verify Evidence

Before analysis, preserve the chain of custody:

`cd ~/evidence/incident # Verify hash integrity sha256sum -c checksums.txt`

**Document:**

- Date/time of evidence acquisition
- Hash values matching originals
- Storage location of evidence
- Who handled the evidence (you)

---

### Step 2 — Establish What "Normal" Looks Like

Before identifying anomalies, understand baseline traffic:

`# Check typical web traffic patterns head -100 apache_access.log.bak | awk '{print $1}' | sort | uniq -c | head -10 # Review when the server typically receives traffic cat apache_access.log.bak | awk '{print $4}' | cut -d' ' -f2 | sort | uniq -c # Check auth.log for normal login patterns tail -50 auth.log.bak | grep -v "Failed password" | head -20`

**Document:** What does routine traffic look like? Are there recognizable patterns?

---

### Step 3 — Identify Anomalous Events

Use multiple approaches to find suspicious activity:

**3a. Detect port scans:**

`# Look for rapid connections to many ports grep -i "scan\|probe\|Nmap" suricata_alerts.log.bak # Or check syslog for unusual connection patterns grep "SYN" /var/log/syslog | head -20`

**3b. Detect failed logins (brute force):**

`# Count failed SSH attempts grep "Failed password" auth.log.bak | wc -l # See the actual failures grep "Failed password" auth.log.bak | tail -20`

**3c. Detect web probing:**

`# Look for sensitive path probes grep "\.git\|\.env\|admin\|config\|passwd" apache_access.log.bak # Check for unusual HTTP methods awk '{print $6}' apache_access.log.bak | sort | uniq -c`

**3d. Detect suspicious files:**

`# Check for unusual files in /tmp ls -la /tmp/ # Look for files with recent modification times find /tmp -type f -mtime -1`

---

### Step 4 — Build a Preliminary Timeline

Start with what you've found and organize chronologically:

|Time (approx.)|Event|Evidence Source|Confidence|
|---|---|---|---|
|?|Reconnaissance started|Suricata/Nmap detection|?|
|?|Web probing detected|Apache logs|?|
|?|SSH brute-force began|Auth logs|?|
|?|Suspicious file created|File timestamp|?|
|?|Session ended|Last log entry|?|

Fill this table with your best estimates. You'll refine it in subsequent steps.

---

### Step 5 — Deep-Dive Analysis with Packet Capture

Open `incident_capture.pcap` in Wireshark:

**5a. Find the scanner:**

Filter: `tcp.flags.syn == 1 && tcp.flags.ack == 0`

Look for source IPs connecting to many ports in short time spans. Document:

- Which IP performed the scan?
- How many unique destination ports?
- Time span of scanning activity?

**5b. Trace web application probing:**

Filter: `http.request.uri contains ".git" or http.request.uri contains ".env"`

Document:

- Which URI paths were probed?
- What User-Agent strings were used?
- Were any responses successful (HTTP 200)?

**5c. Track SSH activity:**

Filter: `tcp.port == 22`

Count SYN packets and note patterns indicating brute force behavior.

**5d. Look for data transfer:**

Filter: `frame.len > 1500 && ip.src == <server-IP>`

Large outbound transfers may indicate exfiltration.

---

### Step 6 — Complete Root Cause Analysis

Answer these questions based on your findings:

|Question|Answer|Supporting Evidence|
|---|---|---|
|Who initiated the attack?|Source IP / identity|Log entry reference|
|What was the attack vector?|Port scan → SSH brute force, etc.|Suricata alert reference|
|Was any unauthorized access achieved?|Yes/No + explanation|Auth log entries|
|What systems/data were compromised?|File paths, services|File timestamps + hashes|
|What was the likely motivation?|Recon, credential theft, etc.|Attack pattern analysis|
|What control failures allowed this?|Missing logging, no rate limiting, etc.|Control gap identification|
|What would have prevented this?|Recommendations|Security improvement plan|

---

### Step 7 — Write the Incident Report

Produce a formal incident report:

`# INCIDENT INVESTIGATION REPORT ## 1. Executive Summary [Brief overview of incident, impact, and key findings] ## 2. Scope of Investigation - Systems examined: [list] - Timeframe: [start] to [end] - Evidence sources consulted: [list] ## 3. Timeline of Events [Chronological reconstruction with evidence references] ## 4. Findings ### 4.1 Attack Vector [What was the initial entry point?] ### 4.2 Compromise Details [Was unauthorized access achieved? What data/files accessed?] ### 4.3 Evidence Summary | Evidence Type | Location | Key Finding | |---------------|----------|-------------| | Apache logs | access.log.bak | ... | | Auth logs | auth.log.bak | ... | | Suricata alerts | fast.log.bak | ... | | Packet capture | incident_capture.pcap | ... | ## 5. Root Cause Analysis ### 5.1 Technical Root Cause [Configuration weakness, missing control, etc.] ### 5.2 Process Root Cause [Why wasn't this detected earlier? What gaps existed?] ## 6. Impact Assessment - Systems affected: - Data potentially compromised: - Business impact: ## 7. Containment Actions Taken [If applicable] ## 8. Remediation Recommendations ### Short-Term (Immediate) 1. [Action] - Priority: High 2. [Action] - Priority: High ### Long-Term 1. [Action] - Priority: Medium 2. [Action] - Priority: Low ## 9. Lessons Learned [What would prevent similar incidents?] ## 10. Appendices - Full log excerpts - PCAP summary statistics - Hash verification records`

Save as `mission01-lab11-incident-report.md`.

---

## Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Chain-of-custody documentation|Part of technical report|
|Preliminary timeline|Incident reconstruction|
|Root cause analysis table|Root-cause analysis|
|Formal incident report|Incident reconstruction|
|Evidence hash verification record|Part of technical report|

---

## Success Criteria

- ✅ All evidence preserved with hash verification
- ✅ Timeline is complete and each event maps to at least one piece of evidence
- ✅ Root cause clearly identified and supported by analysis
- ✅ Incident report follows professional structure
- ✅ Learner can articulate what control failures allowed the incident
- ✅ Remediation recommendations are specific and actionable