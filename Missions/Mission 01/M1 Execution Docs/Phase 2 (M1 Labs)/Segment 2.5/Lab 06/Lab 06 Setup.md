## LAB 06 — Routing Failure

### Objective

Deliberately break routing in the lab topology and systematically diagnose the failure. Learn to distinguish network-layer failures from security-control failures — a critical investigative skill.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|3.4-A|High availability|🟢 Demonstrated|Redundancy analysis and failure impact documentation|
|3.4-C|Testing for resilience/recovery|🟢 Demonstrated|Deliberate failure injection and recovery testing|
|1.3-B|Technical implications of changes|🟢 Demonstrated|Change → failure → diagnosis → restoration documented|
|4.8-D|Root cause analysis|🟢 Demonstrated|Systematic root-cause identification from symptoms|
|2.5-E|Isolation|🟢 Demonstrated|Fault isolation through systematic testing|
|3.4-G|Continuity of operations|🟡 Understood|Impact of single points of failure analyzed|

### Prerequisites

Lab 02 complete.

### Tools

- Packet Tracer (Lab 02 topology)
- draw.io

### Procedure

**Step 1 — Establish the baseline**

1. Open the Lab 02 Packet Tracer file. Save as `mission01-lab06-routing-failure.pkt`.
2. Verify baseline connectivity: `ping 172.16.0.10` from PC0. Record the result.
3. Document the working state: routing tables on each router.

To view a routing table:

`enable show ip route`

Save this output — it is your baseline evidence.

**Step 2 — Inject Failure A: Remove a route**

On Router0 (the carrier edge):

`configure terminal no ip route 172.16.0.0 255.255.255.0 10.0.0.2 end`

Now test: `ping 172.16.0.10` from PC0.

**Step 3 — Diagnose without prior knowledge**

Pretend you did not make this change. Systematically investigate:

1. **Physical/Link layer check:** Can PC0 reach its own gateway? `ping 192.168.10.1` — if yes, the link is fine.
2. **Next-hop check:** Can PC0 ping the far side of the first link? `ping 10.0.0.2` — if this fails, the problem is between the edge and core.
3. **Route table inspection:** Check `show ip route` on each router. Compare with baseline. Which router is missing which route?
4. **Traceroute:** From PC0 → Command Prompt → `tracert 172.16.0.10`. Where does the trace stop?

Document each diagnostic step, what it revealed, and how it narrowed the problem.

**Step 4 — Restore and validate**

`configure terminal ip route 172.16.0.0 255.255.255.0 10.0.0.2 end`

Verify: `ping 172.16.0.10` succeeds. Record the restored state.

**Step 5 — Inject Failure B: Shut down an interface**

On Router1 (core router):

`configure terminal interface fa0/0 shutdown end`

Test from PC0: `ping 172.16.0.10`

**Step 6 — Diagnose Failure B**

Repeat the systematic approach:

1. Can PC0 reach its gateway? (Should be yes.)
2. Can PC0 ping the next hop (10.0.0.2)? (Should be no.)
3. What does `show ip route` show on Router0? Does the route still exist?
4. What does `show interface fa0/0` show on Router1? What state is the interface in?

Key insight: The routing table may still have the route, but the interface is down. How does this differ from Failure A?

**Step 7 — Restore and validate**

`configure terminal interface fa0/0 no shutdown end`

Verify connectivity is restored.

**Step 8 — Inject Failure C: Misconfigured ACL (security-control failure)**

On Router0:

`configure terminal access-list 101 deny ip 192.168.10.0 0.0.0.255 172.16.0.0 0.0.0.255 access-list 101 permit ip any any interface fa0/1 ip access-group 101 out end`

Test from PC0: `ping 172.16.0.10`

This should fail — but for a different reason than routing. The route exists, the interfaces are up, but traffic is being dropped by a security policy.

**Step 9 — Diagnose Failure C — distinguishing security from routing**

1. Ping the gateway: succeeds (local network fine).
2. Ping the next hop (10.0.0.2): succeeds (routing to the edge is fine).
3. Ping the server (172.16.0.10): fails.
4. Check routing tables: all routes present. So this is NOT a routing failure.
5. Check for ACLs: `show access-lists` on Router0. What do you see?
6. Key question: Without seeing the ACL configuration, how would you know this is a security drop vs. a routing problem?

Document the diagnostic pattern that distinguishes:

- **Routing failure:** Interfaces up, routes missing, traceroute stops at a specific hop
- **Interface failure:** Interface state shows down/up-down, traceroute stops at the failed device
- **Security control:** Everything appears healthy but traffic is silently dropped; traceroute may show partial success then stop at the enforcing device

**Step 10 — Remove the ACL and validate**

`configure terminal interface fa0/1 no ip access-group 101 out no access-list 101 end`

Verify connectivity is fully restored.

**Step 11 — Document a failure taxonomy**

Create a table in your technical report:

|Symptom|Possible Cause|Diagnostic Step|Distinguishing Evidence|
|---|---|---|---|
|Cannot reach destination|Missing route|`show ip route`|Route absent from table|
|Cannot reach destination|Interface down|`show interface`|Interface state = down|
|Cannot reach destination|ACL blocking|`show access-lists`|Route present, interface up, but drops occur|
|Cannot reach destination|DNS failure|`dig` / `nslookup`|IP works but hostname doesn't resolve|

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Baseline routing table output|Routing-failure analysis|
|Failure diagnosis documentation (3 failures)|Routing-failure analysis|
|Failure taxonomy table|Part of technical report|
|Restoration and validation evidence|Part of technical report|

### Success Criteria

- Three distinct failures were injected, diagnosed, and resolved
- Learner can articulate the diagnostic pattern that distinguishes routing, interface, and security-control failures
- All restorations were validated with ping
- Failure taxonomy table is complete and accurate

### Curiosity Branches

- How would dynamic routing protocols (OSPF, BGP) change failure behavior?
- What happens if you add a redundant link? Does traffic automatically fail over?