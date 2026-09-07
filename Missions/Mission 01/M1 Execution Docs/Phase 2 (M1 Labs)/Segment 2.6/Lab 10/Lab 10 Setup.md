## LAB 10 — Monitoring and Investigation

### Objective

Generate controlled activity on the lab network and investigate it using multiple correlated evidence sources. Develop the ability to piece together a timeline of events from disparate log sources.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.4-A|Monitoring tools|🟢 Demonstrated|Multiple monitoring tools deployed and correlated|
|4.4-B|Computing resource activities|🟢 Demonstrated|System and network activity monitored and interpreted|
|4.9-A|Log data for investigations|🟢 Demonstrated|Logs from multiple sources correlated into a timeline|
|4.9-B|Other data sources|🟢 Demonstrated|Packet captures, endpoint data, and network metadata used|
|4.1-G|Monitoring computing resources|🟢 Demonstrated|Resource activity observed and explained|
|4.8-E|Threat hunting|🟡 Understood|Hypothesis-driven search for suspicious activity|
|1.1-F|Detective controls|🟢 Demonstrated|Monitoring and alerting as detective control|

### Prerequisites

Lab 09 complete.

### Tools

- Ubuntu Server VM (target + collector)
- Nmap (to generate network activity)
- Apache2 (for web logs)
- Suricata (IDS)
- Wireshark / tcpdump (for packet capture)
- Python 3 (for log parsing/correlation)
- draw.io (for timeline diagram)

### Environment Setup

**1. Set up the monitoring stack:**

On the Ubuntu VM:

`# Install Apache (if not already from Lab 09) sudo apt install apache2 # Install Suricata IDS sudo apt install suricata # Enable Apache access and error logging (enabled by default) # Verify logs exist: ls /var/log/apache2/`

**2. Configure Suricata with a basic ruleset:**

`# Update Suricata rules sudo suricata-update # Start Suricata on the VM's interface sudo suricata -i enp0s3 -c /etc/suricata/suricata.yaml -D # Verify it's running sudo systemctl status suricata`

**3. Enable Packet Tracer logging (simulation):**

In the Packet Tracer topology, the ACL logging from Lab 07 should still be active on Router0.

### Procedure

**Step 1 — Establish a monitoring baseline**

Before generating activity, document what "normal" looks like:

`# Check Apache access log (should be mostly empty or baseline traffic) tail /var/log/apache2/access.log # Check Suricata fast log tail /var/log/suricata/fast.log # Check system auth log tail /var/log/auth.log`

Record this as your baseline.

**Step 2 — Generate controlled activity**

Execute the following sequence and record timestamps for each action:

|Time|Action|Expected Evidence Source|
|---|---|---|
|T+0|`curl http://<server-IP>/`|Apache access log|
|T+1|`nmap -sS <server-IP>`|Suricata alerts, auth log|
|T+2|`curl http://<server-IP>/nonexistent`|Apache access log (404)|
|T+3|`ssh invaliduser@<server-IP>`|Auth log (failed login)|
|T+4|`nmap -sV -p 80,443,22 <server-IP>`|Suricata, Apache|
|T+5|`curl http://<server-IP>/`|Apache access log|

Note: Use `date` before each action to record accurate timestamps.

**Step 3 — Begin a packet capture during activity generation**

On a separate terminal:

`# Capture all traffic on the interface sudo tcpdump -i enp0s3 -w mission01-lab10-activity.pcap &`

Run the activity sequence from Step 2, then stop the capture:

`sudo killall tcpdump`

**Step 4 — Collect evidence from all sources**

**4a. Apache access log:**

`cat /var/log/apache2/access.log | tail -20`

Document: Which requests were logged? What information does each entry contain? (IP, timestamp, request, response code, user agent)

**4b. Apache error log:**

`cat /var/log/apache2/error.log | tail -20`

**4c. Suricata alerts:**

`cat /var/log/suricata/fast.log | tail -20`

Document: Did Suricata flag the Nmap scan? What signatures triggered? What information does each alert contain?

**4d. Authentication log:**

`grep "sshd" /var/log/auth.log | tail -20`

Document: Was the failed SSH login attempt logged? What information is recorded?

**4e. System journal:**

`journalctl --since "1 hour ago" | grep -i "accept\|fail\|deny"`

**4f. Packet capture:** Open `mission01-lab10-activity.pcap` in Wireshark. Identify:

- The Nmap scan pattern (many SYN packets to different ports)
- The HTTP requests and responses
- The SSH connection attempt
- DNS queries (if any)

**Step 5 — Correlate into a timeline**

Create a chronological timeline combining all sources:

|Timestamp|Event|Source|Details|
|---|---|---|---|
|T+0|HTTP GET /|Apache access log|200 OK, source IP: [client]|
|T+1|Port scan detected|Suricata fast.log|SID: xxx, "Nmap scan"|
|T+2|HTTP GET /nonexistent|Apache access log|404 Not Found|
|T+3|Failed SSH login|auth.log|Invalid user "invaliduser"|
|T+4|Service scan|Suricata + Apache|Port 22, 80, 443 probed|
|T+5|HTTP GET /|Apache access log|200 OK|

In draw.io, create a visual timeline showing how different evidence sources contribute to different parts of the same event sequence.

**Step 6 — Threat hunting exercise**

Form a hypothesis and hunt:

> **Hypothesis:** An attacker performed reconnaissance against the web server, followed by an attempted login.

Using your collected evidence:

1. Which log source first shows the recon activity?
2. How quickly did the SSH attempt follow the scan?
3. What source IP was used? Is it consistent across events?
4. Was any successful access achieved?
5. What would alerting thresholds look like for this activity?

Document your findings as a short hunting report.

**Step 7 — Packet Tracer correlation**

Return to the Packet Tracer topology:

1. Check Router0 logging (`show logging`) — were any ACL denies logged during your activity?
2. Compare what Packet Tracer logs vs. what the real Linux VM logs.
3. Document: What evidence sources exist in real networks that Packet Tracer cannot provide?

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Multi-source log collection|Monitoring evidence|
|Activity timeline (table + draw.io diagram)|Monitoring evidence|
|Packet capture of generated activity|Packet captures|
|Threat hunting report|Part of technical report|
|Source-comparison analysis (Packet Tracer vs real VM)|Part of technical report|

### Success Criteria

- Multiple evidence sources were collected and correlated into a single timeline
- Each event in the timeline maps to at least one log source
- Learner can explain what each monitoring tool contributes
- Threat hunting hypothesis was tested with evidence