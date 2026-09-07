## LAB 02 — Build the Carrier-Like Network

### Objective

Expand Lab 01's simplified topology into a carrier-like multi-tier network with aggregation, core routing, segmentation, and security control placement points. This models the journey through a cellular carrier's network.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|3.2-A|Infrastructure considerations|🟢 Demonstrated|Multi-tier topology with aggregation/core/edge layers|
|3.2-B|Control selection|🟢 Demonstrated|Security control placement justified at each tier|
|2.5-A|Segmentation|🟢 Demonstrated|Separate VLANs/subnets for access, aggregation, core|
|1.1-A|Technical controls|🟢 Demonstrated|Technical control placement documented|
|1.1-E|Operational controls|🟢 Demonstrated|Operational control reasoning documented|
|4.1-A|Secure baselines|🟢 Demonstrated|Device hardening checklist applied to routers|

### Prerequisites

Lab 01 complete.

### Tools

- Packet Tracer
- draw.io

### Environment Setup

**Expanded topology:**

`Client PCs (2-3) │ Access Switch (with VLANs) │ Aggregation Switch │ Edge Router (Carrier Edge — NAT, ACLs) │ Core Router (Carrier Core) │ Peering Router (Internet Edge) │ Destination Switch │ Web Server + DNS Server`

### Procedure

**Step 1 — Build the expanded topology in Packet Tracer**

1. Start from the Lab 01 file (save as `mission01-lab02-carrier-network.pkt`).
2. Add a second PC to the access switch.
3. Insert an aggregation switch between the access switch and the carrier edge router.
4. Add a DNS server alongside the web server at the destination.
5. Add labels to each device naming its real-world counterpart:
    - Access Switch = "RAN/gNodeB area"
    - Aggregation Switch = "Carrier transport aggregation"
    - Edge Router = "Carrier edge / NAT gateway"
    - Core Router = "Carrier core network"
    - Peering Router = "Internet peering point"

**Step 2 — Implement VLAN segmentation**

On the access switch:

`enable configure terminal vlan 10 name CLIENT_DATA vlan 20 name MANAGEMENT vlan 30 name SERVER_FARM exit`

Assign ports:

- Ports connected to PCs → VLAN 10
- Port toward aggregation → trunk (allow all VLANs)

**Step 3 — Subnet the address space**

|Segment|VLAN|Subnet|Purpose|
|---|---|---|---|
|Client access|10|192.168.10.0/24|Client devices|
|Management|20|192.168.20.0/24|Switch/router management|
|Server farm|30|172.16.0.0/24|DNS + Web server|
|Carrier backbone|—|10.0.0.0/30 (links)|Inter-router links|

**Step 4 — Configure inter-VLAN routing on the edge router (Router-on-a-Stick)**

On the Edge Router:

`enable configure terminal interface fa0/0 no shutdown interface fa0/0.10 encapsulation dot1q 10 ip address 192.168.10.1 255.255.255.0 interface fa0/0.20 encapsulation dot1q 20 ip address 192.168.20.1 255.255.255.0 interface fa0/0.30 encapsulation dot1q 30 ip address 172.16.0.1 255.255.255.0`

**Step 5 — Configure static routes on all routers**

Ensure every router knows how to reach every subnet. Add static routes as needed.

**Step 6 — Configure the DNS server**

1. Click the DNS Server → Services → DNS.
2. Set DNS service to On.
3. Add a record: Name = `google.local`, Address = `172.16.0.10` (web server IP).
4. Set the DNS server IP to `172.16.0.20`.

**Step 7 — Configure PC DNS settings**

1. On each PC → Desktop → IP Configuration.
2. Set DNS Server to `172.16.0.20`.

**Step 8 — Test name resolution and HTTP**

1. From PC0 → Web Browser → navigate to `http://google.local`.
2. Confirm the page loads.
3. From PC0 → Command Prompt → `ping google.local`. Confirm DNS resolves to 172.16.0.10.

**Step 9 — Apply secure baselines (hardening)**

On each router:

`! Disable unused services no service dhcp no ip http server no cdp run ! Set passwords enable secret class line console 0 password cisco login line vty 0 4 password cisco login ! Banner banner motd ^C AUTHORIZED ACCESS ONLY ^C`

Document each hardening action and why it matters.

**Step 10 — Annotate security control placement points**

In draw.io, create an expanded diagram showing:

- Where a firewall would go (and why)
- Where an IDS/IPS sensor would sit
- Where DNS filtering could operate
- Where NAT occurs
- Where monitoring/logging should collect

Write a one-paragraph justification for each placement decision.

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Expanded Packet Tracer topology|Level 2 carrier architecture|
|Updated draw.io diagram with control placements|Security-control analysis|
|Hardening checklist document|Part of Mission 01 technical report|
|Written control-placement justification|Security-control analysis|

### Success Criteria

- Both PCs can resolve `google.local` via DNS
- Both PCs can load the web page
- VLAN segmentation is functional (PCs in VLAN 10 cannot directly reach management VLAN 20 without routing)
- Hardening checklist is applied and documented
- Learner can explain the function of each tier and why segmentation matters for security

### Curiosity Branches

- What happens if you remove the DNS server? Can clients still reach the web server by IP?
- What happens if you misconfigure the trunk port to carry only VLAN 10?
- Could you add an ACL on the edge router to block ICMP from the client VLAN to the server VLAN? What would the effect be?