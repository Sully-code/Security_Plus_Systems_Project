## LAB 07 — Terminal Diagnostics

### Objective

Investigate what diagnostic information is available from satellite terminals and public measurement platforms. Understand what metrics are collected, what they reveal about system health, and how they could support security investigations.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.4-A|Monitoring tools|🟢 Demonstrated|Diagnostic tools and public metrics analyzed|
|4.4-B|Computing resource activities|🟢 Demonstrated|Metrics collection and interpretation|
|4.9-A|Log data for investigations|🟢 Demonstrated|Diagnostic log analysis for investigation|
|4.9-B|Other data sources|🟢 Demonstrated|Signal strength, satellite IDs, obstruction maps|
|4.2-D|Asset monitoring|🟢 Demonstrated|Terminal registration and tracking discussed|
|4.1-G|Monitoring computing resources|🟢 Demonstrated|Link quality and system health monitoring|
|1.1-F|Detective controls|🟢 Demonstrated|Anomaly detection from diagnostic data|

### Prerequisites

Labs 01, 05, 06 complete.

### Tools

- Web browser
- Ookla Speedtest (web-based, free)
- Python 3 (for data analysis)
- Starlink app documentation (public — even without a terminal, the app's features are documented online)
- draw.io

### Procedure

**Step 1 — Research available diagnostic data**

Document what diagnostic information the Starlink system exposes:

**User-facing (via Starlink app):**

- Download/upload speed (on-demand and historical)
- Latency (on-demand and historical)
- Obstruction map (sky view showing blocked areas)
- Uptime/downtime statistics
- Network status (connected, searching, obstructed)
- Firmware version
- Signal strength (if exposed)
- Temperature (terminal)
- Connected devices (router management)

**Network-facing (internal to SpaceX, but documented):**

- Anonymized ping measurements every 15 seconds
- Speed test measurements
- Signal quality metrics
- Satellite handover events
- Beam assignment data

**Third-party public data:**

- Ookla Speedtest aggregated reports (ookla.com/articles)
- Reddit r/Starlink user-reported data (qualitative)
- Downdetector outage reports
- starlink.sx satellite tracking data

**Step 2 — Analyze public performance data**

Using Ookla's public satellite broadband report and Starlink's own network updates:

1. Access ookla.com/articles and find the most recent satellite broadband performance report
    
2. Document:
    
    - Median latency by country/region
    - Median download/upload speeds
    - Latency distribution (what percentage of users see <30ms, <50ms, <100ms?)
    - Comparison to GEO satellite providers
    - Trends over time (has latency improved?)
3. Access starlink.com/updates
    
4. Document:
    
    - Most recent performance claims
    - Number of active satellites/customers
    - Any announced infrastructure changes

**Step 3 — Create a diagnostic data model**

In draw.io, create a diagram showing what data flows where:

`USER TERMINAL ├── Every 15 sec: anon ping measurement → SpaceX NOC ├── On-demand: speed test → nearest test server ├── Continuous: obstruction scan → local display ├── Continuous: signal strength → local display ├── Event: handover → internal log └── Event: obstruction detected → local alert + NOC GATEWAY STATION ├── Continuous: traffic volume → NOC ├── Continuous: link quality per beam → NOC ├── Event: hardware failure → alarm → NOC └── Continuous: power status → NOC SATELLITE ├── Continuous: telemetry → ground stations → NOC ├── Continuous: orbit position → tracking network ├── Event: anomaly → alert → NOC └── Event: command execution → audit log`

For each data stream, document:

- Who can see it? (User, SpaceX only, public?)
- What security value does it have? (Investigation, anomaly detection, capacity planning)
- Could it be used for attack? (Reconnaissance, timing attacks)

**Step 4 — Simulate a diagnostic investigation**

Scenario: A user reports intermittent connectivity drops. Using the diagnostic data model from Step 3, walk through the investigation:

1. **Check the obstruction map:** Is the dish partially blocked by trees or buildings?
2. **Check the latency history:** Are there periodic spikes that correlate with satellite handover?
3. **Check the speed test history:** Has throughput degraded over time?
4. **Check weather data:** Do drops correlate with rain events?
5. **Check firmware version:** Is the terminal running outdated firmware with known bugs?
6. **Check uptime statistics:** What percentage of time is the terminal connected?

Create a diagnostic report template:

`# Diagnostic Investigation Report ## User Complaint [Description of reported issue] ## Terminal Information - Model: [Gen 2/3/Mini] - Firmware: [version] - Installation date: [if known] - Mount type: [roof/pole/tripod] ## Diagnostic Findings ### Obstruction Analysis - Obstruction percentage: [%] - Primary obstructions: [trees/buildings/other] - Recommendation: [reposition/clear/accept] ### Latency Analysis - Median latency: [ms] - Peak latency: [ms] - Spike frequency: [events/hour] - Correlation with handover: [yes/no] ### Throughput Analysis - Median download: [Mbps] - Median upload: [Mbps] - Degradation trend: [stable/declining/improving] ### Environmental Factors - Weather during drops: [clear/rain/snow] - Temperature: [within range/abnormal] ### Root Cause (Probable) [Based on evidence above] ### Recommended Actions 1. [Action] 2. [Action]`

**Step 5 — Analyze the security value of diagnostic data**

Document how diagnostic data supports security operations:

|Data Type|Security Value|Example Use Case|
|---|---|---|
|Latency spikes|Anomaly detection — unexpected spikes may indicate interference or attack|Detecting localized jamming|
|Handover events|Behavioral baseline — abnormal handover patterns may indicate spoofing|Detecting rogue satellite signals|
|Signal strength|Environmental baseline — sudden drops without weather cause may indicate jamming|Detecting deliberate RF interference|
|Firmware version|Vulnerability management — outdated firmware may have known exploits|Patching before exploitation|
|Connected devices|Asset monitoring — unexpected devices on the local network may indicate compromise|Detecting unauthorized access|
|Traffic volume|Data exfiltration detection — unusual outbound volume may indicate compromise|Detecting malware beaconing|

**Step 6 — Compare with Mission 01 monitoring**

Recall Mission 01 Lab 10 (Monitoring and Investigation). Compare what was monitorable in the Packet Tracer/VM environment vs. what is monitorable in the satellite environment:

|Monitoring Capability|Mission 01 (VM/Packet Tracer)|Mission 02 (Satellite)|
|---|---|---|
|Packet capture|Full (Wireshark)|Not available (RF link encrypted, no access point)|
|System logs|Full (auth.log, Apache)|Limited (app-level only)|
|Network logs|Full (ACL logs, Suricata)|Not available (gateway internal)|
|Performance metrics|Full (cpu, mem, network)|Partial (latency, speed, signal)|
|Alert generation|Full (Suricata, custom)|Limited (obstruction alerts)|

Key finding: The satellite user has far less visibility into network internals than a VM lab operator. Security monitoring in satellite systems depends more on the operator (SpaceX) than the end user.

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Diagnostic data inventory|Diagnostic metrics collection|
|Public performance data analysis|Part of technical report|
|Diagnostic data flow diagram (draw.io)|Part of diagnostic report|
|Diagnostic investigation report template|Part of technical report|
|Security value of diagnostic data table|Part of technical report|
|Mission 01 vs Mission 02 monitoring comparison|Part of technical report|

### Success Criteria

- All diagnostic data sources are documented with their accessibility level
- Public performance data is cited from specific sources
- Diagnostic report template is practical and complete
- Learner can explain why satellite users have less monitoring visibility than lab operators
- Security value of each data type is mapped to Security+ requirements

### Curiosity Branches

- What is the Starlink "grub" (gRPC) API that some community tools use to query terminal data?
- How does SpaceX's NOC monitor 10,000+ satellites simultaneously?
- What is network telemetry and how does it differ from logging?
- Could an attacker manipulate diagnostic data to hide their activities?