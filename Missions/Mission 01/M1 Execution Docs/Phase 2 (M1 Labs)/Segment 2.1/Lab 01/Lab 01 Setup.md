Build the Simplified Journey

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

## LAB 01 — Build the Simplified Journey

### Objective

Build a minimal end-to-end network topology in Packet Tracer representing the simplified Phone → Google journey. Establish the conceptual model physically before adding complexity.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|3.2-A|Infrastructure considerations|🟢 Demonstrated|Working multi-segment topology with distinct functional zones|
|3.2-D|Secure access|🟢 Demonstrated|Access-control reasoning across zones documented|
|2.5-A|Segmentation|🟢 Demonstrated|Distinct network segments for client, access, core, destination|

### Prerequisites

None — this is the first lab.

### Tools

- Packet Tracer
- draw.io (diagrams.net)

### Environment Setup

**Packet Tracer topology:**

`PC0 (representing phone) │ Switch (Access) │ Router0 (Carrier/ISP Edge) │ Router1 (Internet hop) │ Switch (Destination) │ Server0 (representing Google — HTTP service enabled)`

### Procedure

**Step 1 — Build the topology**

1. Open Packet Tracer. Create a new file.
2. Place: 1 PC, 2 generic switches, 2 generic routers, 1 server.
3. Connect them with copper straight-through cables as shown above.

**Step 2 — Assign IP addresses (manual)**

|Device|Interface|IP Address|Subnet|
|---|---|---|---|
|PC0|Fa0|192.168.10.10|/24|
|Router0|Fa0/0 (toward PC)|192.168.10.1|/24|
|Router0|Fa0/1 (toward Router1)|10.0.0.1|/30|
|Router1|Fa0/0 (toward Router0)|10.0.0.2|/30|
|Router1|Fa0/1 (toward Server)|172.16.0.1|/24|
|Server0|Fa0|172.16.0.10|/24|

**Step 3 — Configure default gateways**

- PC0 gateway: 192.168.10.1
- Server0 gateway: 172.16.0.1

**Step 4 — Enable HTTP on Server0**

1. Click Server0 → Services tab → HTTP.
2. Ensure HTTP service is set to On.

**Step 5 — Test connectivity**

1. From PC0, open the Desktop → Command Prompt.
2. Ping the Server0 IP: `ping 172.16.0.10`
3. If ping fails, troubleshoot routing (see Lab 06 for systematic failure analysis).

**Step 6 — Add static routes**

On Router0:

`enable configure terminal ip route 172.16.0.0 255.255.255.0 10.0.0.2 end write memory`

On Router1:

`enable configure terminal ip route 192.168.10.0 255.255.255.0 10.0.0.1 end write memory`

**Step 7 — Test HTTP access**

1. From PC0 → Desktop → Web Browser.
2. Navigate to `http://172.16.0.10`.
3. Confirm the default Packet Tracer web page loads.

**Step 8 — Document the architecture**

1. Save the Packet Tracer file as `mission01-lab01-simple-journey.pkt`.
2. In draw.io, create a clean diagram showing:
    - Each device and its role
    - IP addressing scheme
    - Network segment boundaries
    - Trust boundary annotations (where does the "carrier" zone end?)
3. Add a written summary: What does each segment represent in the real Phone → Google journey?

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Packet Tracer topology file|Simplified network topology|
|draw.io architecture diagram|Level 1 architecture diagram|
|Written segment/role summary|Part of Mission 01 technical report|

### Success Criteria

- Ping succeeds from PC0 to Server0
- HTTP page loads from PC0's browser
- Diagram clearly labels each segment's real-world equivalent
- Learner can explain what happens at each hop in plain language

### Curiosity Branches

- What happens if you add a second PC on the same switch? Can they communicate? Why or why not without a router?
- What happens if Server0 has no default gateway but PC0 tries to reach it anyway?