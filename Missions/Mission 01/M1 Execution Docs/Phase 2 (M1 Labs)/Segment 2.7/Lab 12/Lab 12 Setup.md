# LAB 12 — END-TO-END RECONSTRUCTION

### Objective

Reconstruct the complete **Phone → Google** journey from scratch using only evidence gathered throughout Mission 01. This is the **capstone synthesis exercise** demonstrating end-to-end systems understanding.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|1.2-A|Confidentiality|🟢 Demonstrated|End-to-end confidentiality mechanism traced|
|1.2-B|Integrity|🟢 Demonstrated|Integrity protection points identified|
|1.2-E|Authentication|🟢 Demonstrated|Authentication points across the journey mapped|
|1.2-F|Authorization|🟢 Demonstrated|Authorization decisions documented|
|1.4-A|PKI|🟢 Demonstrated|Certificate trust path validated|
|1.4-B|Encryption|🟢 Demonstrated|Encryption layers identified and explained|
|2.2-H|Attack surfaces|🟢 Demonstrated|Attack surface map completed end-to-end|
|3.2-C|Secure communication|🟢 Demonstrated|Communication security at each layer documented|
|3.2-D|Secure access|🟢 Demonstrated|Access control mechanisms across zones mapped|
|4.8-F|Digital forensics|🟢 Demonstrated|Evidence correlation across domains|
|4.9-A|Log data for investigations|🟢 Demonstrated|Logs from each domain identified|
|4.9-B|Other data sources|🟢 Demonstrated|Multiple evidence types synthesized|

### Prerequisites

All Labs 01–11 complete. All evidence files from previous labs should be archived.

### Tools

- All prior evidence files (.pkt, .pcap, logs, reports)
- draw.io (for diagrams)
- Text editor / markdown (for final narrative)

---

## PROCEDURE

### Step 1 — Gather Your Evidence Archive

Create a single evidence repository:

`mkdir ~/mission01-evidence-archive cp ~/mission01-lab*.pkt ~/mission01-evidence-archive/ cp ~/mission01-lab*.md ~/mission01-evidence-archive/ cp ~/mission01-*.pcap* ~/mission01-evidence-archive/ cp ~/evidence/* ~/mission01-evidence-archive/`

This is your **complete evidence corpus**.

---

### Step 2 — Create the Final Architecture Diagrams

Using draw.io, produce these **five required diagrams**:

|Diagram|Purpose|Passport Artifact #|
|---|---|---|
|Level 0|Human view (Phone → Google → Webpage)|#1|
|Level 1|Major system blocks (Smartphone, RAN, Carrier, Internet, Google)|#2|
|Level 2|Detailed carrier architecture (gNodeB, transport, core, edge)|#3|
|Protocol stack|Vertical protocol layers (Application → Physical)|#5|
|Trust boundaries|Where trust is established and breaks|#6|

---

### Step 3 — Map Security+ Concepts Across the Journey

Create a **comprehensive coverage table** linking each atomic requirement to specific evidence:

|Security+ Area|Journey Point(s)|Evidence Source|Confidence|
|---|---|---|---|
|1.2-A Confidentiality|TLS at browser + network|Lab 04, 05 pcap|🟢|
|1.4-A PKI|Certificate validation|Lab 05 OpenSSL|🟢|
|2.5-A Segmentation|VLANs, ACLs|Lab 02, 07|🟢|
|4.3 Vulnerability lifecycle|Identify→Report cycle|Lab 09|🟢|
|4.8 Incident response|Reconstruction from logs|Lab 11|🟢|
|...|...|...|...|

---

### Step 4 — Write the Final Narrative (2,000–4,000 Words)

This is **the core artifact** of Mission 01. Someone should be able to read it and understand how their phone reaches Google without needing any other materials.

**Required structure:**

`# MISSION 01 FINAL EXPLANATION: PHONE → GOOGLE ## Introduction [One paragraph framing the problem] ## Section 1: Before the Request—Phone Preparation - Power state and radio attachment - Identity/authentication on cellular network - IP address assignment - DNS resolver configuration ## Section 2: Application Layer—The Browser - URL parsing and resolution intent - DNS query initiation - HTTPS/TLS session requirements - Certificate store and trust anchors ## Section 3: Cell Tower and Radio Access - 5G NR signal transmission - gNodeB role in connection management - Handover considerations - Physical security of infrastructure ## Section 4: Carrier Core Network - Aggregation to regional routers - NAT translation at carrier edge - Firewall and access control enforcement - Traffic separation between subscribers ## Section 5: Internet Transit - Peering points and route propagation - BGP and path selection - CDN and edge caching role - Latency considerations ## Section 6: Google Infrastructure - Edge servers and load balancers - TLS termination at Google - Application processing - Response generation ## Section 7: The Return Path - Symmetry/asymmetry of routes - Connection state at phone - Content delivery to browser ## Section 8: Security Throughout Where confidentiality, integrity, and authentication are established at each layer, and where vulnerabilities exist. ## Conclusion What makes this system secure? Where are its weaknesses? What could break? What would evidence of compromise look like?`

**Key requirement:** You must cite specific evidence from earlier labs throughout the narrative (e.g., "as seen in the Wireshark capture from Lab 04...", "consistent with the certificate analysis in Lab 05...").

---

### Step 5 — Assemble the Supporting Artifact Package

Export all visual artifacts as PDF/PNG with clear labels:

1. Level 0–2 architecture diagrams
2. Protocol stack diagram
3. Trust boundary diagram
4. Attack surface map
5. Threat-vector map
6. Timeline sample (from Lab 10)
7. Incident report excerpt (from Lab 11)
8. Vulnerability report excerpt (from Lab 09)
9. Firewall configuration (from Lab 07)
10. Packet capture summaries (from Lab 04, 10)

---

### Step 6 — Self-Assessment Against Security+ Coverage

For each atomic requirement marked 🟢 in your Passport coverage table, answer:

|Requirement|Does my evidence prove demonstration?|Gap or confidence issue|
|---|---|---|
|1.2-A Confidentiality|Yes — TLS analysis, packet inspection|None|
|1.4-A PKI|Yes — certificate chain inspection|None|
|...|...|...|

Be honest about weak areas. Adjust coverage claims if necessary.

---

### Step 7 — Reflection and Forward-Looking Assessment

Write a final reflection addressing:

1. **Learning progression:** What did you understand at the start vs. end?
2. **Systems thinking:** How has your ability to reason about complex systems improved?
3. **Security posture:** Can you now identify where security fails in everyday systems?
4. **Evidence literacy:** Can you distinguish strong evidence from speculation?
5. **Remaining gaps:** What Security+ topics still need work in future missions?

---

## ARTIFACTS PRODUCED

|Artifact|Passport Reference|
|---|---|
|Level 0–2 architecture diagrams|#1, #2, #3|
|Protocol stack diagram|#5|
|Trust boundary diagram|#6|
|Attack surface map|#7|
|Threat-vector map|#8|
|Final narrative explanation|#23 — Final "Phone → Google" explanation|
|Supporting artifact archive|#1–23 tangible artifacts|
|Security+ coverage self-assessment|#22 — Security+ atomic coverage record|
|Reflection and gap analysis|Part of technical report|

---

## SUCCESS CRITERIA

- ✅ Narrative flows coherently from user input to page display and back
- ✅ Each major architectural component is named and explained
- ✅ Security concepts (CIA triad, PKI, firewalls, monitoring) embedded throughout
- ✅ At least 10 artifacts assembled into a portfolio
- ✅ Self-assessment identifies weak evidence areas honestly
- ✅ Learner could explain this journey **off-script** to another person