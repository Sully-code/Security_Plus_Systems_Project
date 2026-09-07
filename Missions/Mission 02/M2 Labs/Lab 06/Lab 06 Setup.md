## LAB 06 — Link Failure Simulation

### Objective

Simulate and analyze link failure scenarios in a controlled model environment. Since we cannot trigger real satellite failures, we model failures in Packet Tracer and analyze the behavioral differences between routing failures, link-layer failures, and environmental failures.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|3.4-C|Resilience testing|🟢 Demonstrated|Failure scenarios simulated and analyzed|
|4.8-D|Root cause analysis|🟢 Demonstrated|Systematic diagnosis of simulated failures|
|4.9-A|Log data for investigations|🟢 Demonstrated|Diagnostic log analysis from failure scenarios|
|1.1-H|Corrective controls|🟡 Understood|Restoration and redundancy activation|
|1.3-B|Technical implications of changes|🟡 Understood|Configuration changes during failure recovery|

### Prerequisites

Labs 01 and 02 complete. Mission 01 Lab 06 (Routing Failure) complete.

### Tools

- Packet Tracer
- draw.io
- Python 3 (optional, for timeline generation)

### Environment Setup

Build a simplified satellite network model in Packet Tracer that mirrors the Starlink architecture:

`PC0 (User Device) │ Switch (Local Network) │ Router0 (Starlink Terminal/Router) │ Router1 (Satellite — simulating the relay) │ Router2 (Gateway Station) │ Switch (Destination) │ Server0 (Web Server — HTTP enabled)`

IP addressing:

|Device|Interface|IP Address|Subnet|
|---|---|---|---|
|PC0|Fa0|192.168.1.10|/24|
|Router0|Fa0/0 (toward PC)|192.168.1.1|/24|
|Router0|Fa0/1 (toward Router1)|10.0.0.1|/30|
|Router1|Fa0/0 (toward Router0)|10.0.0.2|/30|
|Router1|Fa0/1 (toward Router2)|10.0.1.1|/30|
|Router2|Fa0/0 (toward Router1)|10.0.1.2|/30|
|Router2|Fa0/1 (toward Server)|172.16.0.1|/24|
|Server0|Fa0|172.16.0.10|/24|

Configure static routes on all routers for full connectivity. Enable HTTP on Server0.

Add a **second path** to simulate redundancy (alternate gateway):

`Router1 (Satellite) also connects to: │ Router3 (Alternate Gateway) │ Switch │ Server0 (same destination, different path)`

Router1 ↔ Router3: 10.0.2.0/30 Router3 → Server0: 172.16.0.0/24 via 10.0.2.2

### Procedure

**Step 1 — Establish baseline**

1. Verify full connectivity: `ping 172.16.0.10` from PC0.
2. Verify HTTP: browse to `http://172.16.0.10`.
3. Save routing tables on all routers: `show ip route`.
4. Document the working state as your baseline.

**Step 2 — Simulate Failure A: Satellite link loss (handover gap)**

On Router0, shut down the interface toward Router1:

`configure terminal interface fa0/1 shutdown end`

This simulates the brief gap when a satellite passes out of view and the terminal hasn't yet locked onto the next one.

Observe:

1. Ping from PC0 to Server0 — what happens?
2. How long does the outage last? (In real Starlink, this would be sub-second to a few seconds)
3. Is TCP affected? (In real life, a brief dropout may cause retransmission but not connection loss)

Restore:

`configure terminal interface fa0/1 no shutdown end`

Document the recovery behavior.

**Step 3 — Simulate Failure B: Gateway outage (traffic rerouting)**

Instead of restoring Router0's interface, let's simulate a gateway failure:

1. First, ensure the alternate path (Router1 → Router3 → Server0) is configured.
2. On Router2 (primary gateway), shut down its interface toward Router1:

`configure terminal interface fa0/0 shutdown end`

3. On Router1, the route to 172.16.0.0/24 via Router2 should fail. Does traffic automatically reroute via Router3?

If not (static routes don't auto-converge):

- Remove the primary route and add the backup route:

`no ip route 172.16.0.0 255.255.255.0 10.0.1.2 ip route 172.16.0.0 255.255.255.0 10.0.2.2`

4. Test: `ping 172.16.0.10` from PC0.

Document:

- How does this compare to real Starlink gateway failover?
- In reality, BGP and dynamic routing protocols handle this automatically
- What is the latency penalty of using a more distant gateway?

**Step 4 — Simulate Failure C: Environmental degradation (rain fade)**

Rain fade doesn't cause a hard failure — it degrades the link. Simulate this:

1. Add an ACL that drops a percentage of traffic (simulate packet loss):

`access-list 101 permit ip host 192.168.1.10 host 172.16.0.10`

Actually, Packet Tracer can't simulate probabilistic packet loss easily. Instead:

2. Increase the "distance" metaphorically by adding an additional router hop to simulate increased latency:
    
    - Add Router4 between Router0 and Router1
    - Observe the latency increase in ping times
3. Alternatively, use extended ping with different packet sizes to simulate degraded throughput.
    

Document:

- What does rain fade look like from the user's perspective? (Increased latency, packet loss, reduced throughput)
- How does TCP react to packet loss? (Congestion window reduction, retransmissions)
- How does this differ from a hard failure? (Gradual degradation vs. total outage)

**Step 5 — Simulate Failure D: Terminal power loss**

Simply disconnect PC0's cable from the switch, or shut down PC0.

Document:

- The terminal has no backup power — service is immediately lost
- No logs are generated at the terminal (it's off)
- The network may log the terminal as unreachable
- Compare to Mission 01: a phone has a battery, so it survives brief power interruptions. A Starlink terminal does not.

**Step 6 — Create the failure taxonomy**

Extend the Mission 01 failure taxonomy table:

|Symptom|Possible Cause (Satellite)|Diagnostic Step|Distinguishing Evidence|
|---|---|---|---|
|Cannot reach Internet|Satellite handover gap|Wait and retry|Service restores within seconds|
|Cannot reach Internet|Rain fade|Check weather; check signal strength in app|Degraded but not dead; latency increases|
|Cannot reach Internet|Gateway outage|Check for alternate path activation|Traffic rerouted; latency may increase|
|Cannot reach Internet|Terminal power loss|Check terminal LED/power|Terminal completely dark|
|Cannot reach Internet|Terminal hardware failure|Check terminal diagnostics|Terminal powered but no signal|
|High latency, intermittent drops|RF interference|Check for nearby transmitters|Signal quality metrics abnormal|

Compare with Mission 01's failure taxonomy:

- Mission 01 distinguished routing failures, interface failures, and ACL blocks
- Mission 02 adds environmental failures, power failures, and handover gaps
- Both share: backhaul cuts, DNS failures, server outages

**Step 7 — Document the diagnostic approach**

Write a diagnostic runbook for satellite link failures:

`1. Is the terminal powered? (LED status) ├── No → Check power supply, UPS, outlet └── Yes → Continue 2. Does the terminal see a satellite? (App diagnostics) ├── No → Check for obstructions, reposition dish └── Yes → Continue 3. Can you ping the terminal's local IP? ├── No → Local network problem (Wi-Fi, cable) └── Yes → Continue 4. Can you ping 8.8.8.8 (or any public IP)? ├── No → Satellite link or gateway problem │ ├── Check weather conditions │ ├── Check for known outages (Starlink app/status) │ └── If persistent, contact support └── Yes → Continue 5. Can you resolve DNS? ├── No → DNS resolver problem └── Yes → Continue 6. Can you reach specific website? ├── No → Website-specific or routing problem └── Yes → Intermittent issue, monitor`

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Packet Tracer satellite model (with redundancy path)|Link failure analysis|
|Failure scenario documentation (4 scenarios)|Link failure analysis|
|Extended failure taxonomy table|Part of technical report|
|Diagnostic runbook|Part of technical report|
|Recovery/restoration evidence|Part of technical report|

### Success Criteria

- Four failure scenarios are simulated and documented
- Failure taxonomy extends Mission 01's table with satellite-specific failures
- Diagnostic runbook is systematic and practical
- Learner can distinguish hard failures from degraded performance
- Redundancy path is tested and validated in the Packet Tracer model

### Curiosity Branches

- How would dynamic routing (OSPF, BGP) change the failover behavior in this model?
- What is the difference between "available" and "usable" in the context of rain fade?
- How does QUIC (used by Starlink's transport layer) handle brief link interruptions better than TCP?