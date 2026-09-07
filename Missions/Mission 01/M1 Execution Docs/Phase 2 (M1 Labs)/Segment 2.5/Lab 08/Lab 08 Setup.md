## LAB 08 — DNS Attack Scenario

### Objective

Model a DNS manipulation scenario in the isolated lab. Observe what changes, what evidence appears, what security controls could detect it, and how the user experience is affected. This lab is defensive — the learner observes and detects, not exploits.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|2.2-B|Unsecure network vectors|🟢 Demonstrated|DNS manipulation modeled as network attack vector|
|2.4-E|Network attacks|🟢 Demonstrated|DNS spoofing/poisoning scenario constructed|
|4.5-C|DNS filtering|🟢 Demonstrated|DNS filtering as mitigation deployed and tested|
|4.8-C|Incident response testing|🟢 Demonstrated|Controlled incident scenario executed|
|4.9-A|Log data for investigations|🟢 Demonstrated|DNS manipulation detected from log evidence|
|2.5-A|Segmentation|🟢 Demonstrated|DNS traffic segmented and controlled|
|1.2-A|Confidentiality|🟢 Demonstrated|DNS query interception impact on confidentiality|

### Prerequisites

Lab 07 complete (firewall rules in place).

### Tools

- Packet Tracer (Lab 07 topology)
- Wireshark (for real-world comparison if available)
- draw.io

### Procedure

**Step 1 — Establish the baseline**

1. From the Lab 07 topology, verify: `nslookup google.local` from PC0 returns 172.16.0.10.
2. Verify HTTP to `google.local` loads the web page.
3. Document this as the known-good state.

**Step 2 — Model a DNS poisoning scenario**

In Packet Tracer, modify the DNS server's record:

1. Click the DNS Server → Services → DNS.
2. Edit the `google.local` record: change the IP from `172.16.0.10` to a fictional attacker IP, e.g., `172.16.0.99`.
3. This simulates a compromised or malicious DNS entry.

**Step 3 — Observe the effect**

1. From PC0: `nslookup google.local` — what IP is returned now?
2. From PC0: browse to `http://google.local` — what happens?
3. Document the user experience: the user typed the correct URL but was directed somewhere else (or nowhere).

**Step 4 — Capture evidence**

1. In Simulation Mode, send a DNS query from PC0.
2. Examine the DNS response packet — confirm the malicious IP is in the answer.
3. Document the evidence that would prove DNS was tampered with.

**Step 5 — Implement a mitigation: DNS filtering / ACL**

On Router0, add an ACL that only permits DNS queries to the legitimate DNS server:

`configure terminal access-list 120 permit udp 192.168.10.0 0.0.0.255 host 172.16.0.20 eq 53 access-list 120 permit tcp 192.168.10.0 0.0.0.255 host 172.16.0.20 eq 53 access-list 120 deny udp 192.168.10.0 0.0.0.255 any eq 53 access-list 120 deny tcp 192.168.10.0 0.0.0.255 any eq 53 access-list 120 permit ip any any interface fa0/0.10 ip access-group 120 in end`

This forces all DNS traffic through the approved resolver, preventing a rogue DNS server from being queried.

**Step 6 — Test the mitigation**

1. Attempt to configure a secondary DNS server on PC0 pointing to a different IP.
2. Attempt a DNS query to that secondary server.
3. Document: Does the ACL prevent it? What log evidence appears?

**Step 7 — Restore the legitimate DNS record**

1. On the DNS server, restore `google.local` to `172.16.0.10`.
2. Verify `nslookup google.local` returns the correct IP again.

**Step 8 — Real-world parallel (research + observation)**

Using Wireshark on your own machine:

1. Start capture, filter `dns`.
2. Visit a website.
3. Observe your real DNS queries.
4. Document: Could someone on your network path see your DNS queries? What would that reveal about your browsing?

**Step 9 — Document the attack surface and defense**

Create a diagram in draw.io showing:

- The attack: how DNS manipulation redirects users
- The evidence: what network traces would reveal the manipulation
- The defense: DNS filtering ACLs and approved resolvers
- Remaining risk: What can an attacker still do even with this defense?

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|DNS manipulation scenario documentation|Attack-surface map|
|Evidence of DNS tampering (simulation capture)|Threat-vector map|
|DNS filtering ACL configuration|Firewall/security-policy configuration|
|Mitigation test results|Part of technical report|
|Attack-and-defense diagram (draw.io)|Attack-surface map|

### Success Criteria

- Learner can explain how DNS manipulation redirects users
- Learner has evidence (simulation) showing the before/after DNS response
- DNS filtering mitigation is implemented and tested
- Learner can identify what evidence DNS manipulation would leave in logs
- Diagram clearly shows attack, evidence, and defense layers

### Curiosity Branches

- What is DNSSEC and how does it prevent this type of attack?
- What is DNS over HTTPS (DoH) and how does it change the threat model?
- How does a DNS sinkhole work in enterprise security?