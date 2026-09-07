## LAB 07 — Firewall / Access Control

### Objective

Implement, test, and validate firewall rules on the lab network. Develop the ability to write security policies that enforce least privilege, then verify them through controlled testing.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.5-A|Firewalls|🟢 Demonstrated|Working ACL/firewall rules tested and validated|
|1.1-A|Technical controls|🟢 Demonstrated|Firewall as a technical preventive control|
|1.1-B|Preventive controls|🟢 Demonstrated|Access rules prevent unauthorized traffic|
|1.1-F|Detective controls|🟢 Demonstrated|Logging rules detect denied traffic|
|2.5-B|Access control|🟢 Demonstrated|Least-privilege ruleset implemented|
|2.5-C|Configuration enforcement|🟢 Demonstrated|Security baseline enforced via rules|
|4.1-C|Hardening|🟢 Demonstrated|Unnecessary traffic blocked|
|3.2-B|Control selection|🟢 Demonstrated|Control choices justified|

### Prerequisites

Lab 06 complete (working topology with all failures restored).

### Tools

- Packet Tracer (Lab 02 topology)
- Optionally: pfSense VM for a more realistic firewall experience

### Procedure

**Step 1 — Define the security policy**

Before writing any rules, define what traffic SHOULD be allowed on this network. Write a policy table:

|Source|Destination|Port/Protocol|Action|Reason|
|---|---|---|---|---|
|Client VLAN (192.168.10.0/24)|DNS Server (172.16.0.20)|53/UDP|ALLOW|Clients need DNS|
|Client VLAN (192.168.10.0/24)|Web Server (172.16.0.10)|80/TCP|ALLOW|Clients need HTTP|
|Client VLAN (192.168.10.0/24)|Any|22/TCP|DENY|SSH should not be reachable from clients|
|Client VLAN (192.168.10.0/24)|Management VLAN (192.168.20.0/24)|Any|DENY|Clients must not reach management|
|Any|Any|Any|DENY|Default deny|

**Step 2 — Implement the policy as an ACL on Router0 (Edge Router)**

`enable configure terminal ! Extended ACL — numbered 110 access-list 110 permit udp 192.168.10.0 0.0.0.255 host 172.16.0.20 eq 53 access-list 110 permit tcp 192.168.10.0 0.0.0.255 host 172.16.0.10 eq 80 access-list 110 deny tcp 192.168.10.0 0.0.0.255 any eq 22 access-list 110 deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255 access-list 110 deny ip any any ! Apply to the interface facing the clients (inbound) interface fa0/0.10 ip access-group 110 in end write memory`

**Step 3 — Test each policy rule**

Test 1 — DNS should work:

`# From PC0 ping 172.16.0.20 nslookup google.local 172.16.0.20`

Expected: DNS resolves successfully.

Test 2 — HTTP should work:

`# From PC0 browser http://172.16.0.10`

Expected: Page loads.

Test 3 — SSH should be blocked: Enable SSH on the web server first (Services → SSH → On), then attempt:

`# From PC0 command prompt (if SSH client available) ssh -l admin 172.16.0.10`

Expected: Connection refused/timeout. Document the behavior.

Test 4 — Management VLAN should be unreachable:

`# From PC0 ping 192.168.20.1`

Expected: Request times out.

Test 5 — Default deny (try reaching an address that's not in the allow list):

`# From PC0 ping 10.0.0.2`

Expected: Denied by default-deny rule.

**Step 4 — Enable logging on denied traffic**

`configure terminal access-list 110 deny ip any any log interface fa0/0.10 ip access-group 110 in end`

Generate some denied traffic (e.g., `ping 192.168.20.1` from PC0), then check the router logs:

`show logging`

Document what the log entry looks like and what information it provides for investigation.

**Step 5 — pfSense alternative (optional, more realistic)**

If the learner wants a real firewall experience:

1. Download pfSense ISO (free).
2. Create a VirtualBox VM with 2 network adapters (WAN + LAN).
3. Install pfSense, configure WAN and LAN interfaces.
4. Recreate the same policy table using pfSense's web interface:
    - Firewall → Rules → LAN
    - Add rules matching the policy table
5. Test with a client VM behind the LAN interface.

**Step 6 — Document the control analysis**

Write a one-page analysis covering:

- Which type of control is a firewall? (Technical, preventive, potentially detective)
- What is the principle of least privilege as applied here?
- Why is a default-deny policy stronger than default-allow?
- What does the logging rule add to the security posture?
- What security gap remains even with this firewall in place?

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Security policy table|Firewall/security-policy configuration|
|Working ACL configuration (saved in .pkt)|Firewall/security-policy configuration|
|Test results for each rule|Part of technical report|
|Router log capture showing denied traffic|Monitoring evidence|
|Control analysis document|Security-control analysis|
|(Optional) pfSense configuration screenshots|Firewall/security-policy configuration|

### Success Criteria

- All allow rules permit expected traffic
- All deny rules block expected traffic
- Logging captures denied traffic attempts
- Learner can classify the firewall by control type and explain why
- Default-deny policy is in place and tested

### Curiosity Branches

- What is a stateful firewall vs. a packet-filtering firewall?
- How does a next-generation firewall differ from a traditional ACL?
- What is a DMZ and why might you add one to this topology?