# LAB 10 — COMPARATIVE JOURNEY RECONSTRUCTION

### Objective

Reconstruct the complete Starlink journey from scratch using only evidence gathered throughout Mission 02. Then compare this reconstruction to Mission 01's cellular journey. This is the capstone synthesis exercise demonstrating comparative systems thinking.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|1.2-A|Confidentiality|🟢 Demonstrated|End-to-end confidentiality mechanism traced (RF + TLS)|
|1.2-B|Integrity|🟢 Demonstrated|Integrity protection points identified (link + application)|
|1.2-C|Availability|🟢 Demonstrated|Availability mechanisms across both architectures analyzed|
|3.2-C|Secure communication|🟢 Demonstrated|Communication security at each layer documented (satellite + cellular)|
|3.2-A|Infrastructure considerations|🟢 Demonstrated|Physical and logical infrastructure compared|
|4.1-D|Wireless security|🟢 Demonstrated|RF link security in both architectures compared|
|2.2-H|Attack surfaces|🟢 Demonstrated|Comparative attack surface mapping|
|5.2-A|Risk identification|🟡 Understood|Risks across both systems identified|
|5.2-B|Risk assessment|🟡 Understood|Risk comparison between architectures|
|4.9-B|Other data sources|🟢 Demonstrated|Multi-domain evidence synthesized|

### Prerequisites

All Labs 01–09 complete. Mission 01 complete (all 12 labs).

### Tools

- All evidence files from previous labs
- Mission 01 artifacts (archived)
- Mission 02 artifacts (compiled)
- draw.io (for final diagrams)
- Text editor/markdown (for final narrative)

### Procedure

**Step 1 — Recall the original question**

Revisit Mission 02's starting point:

> **"What actually happens when my Starlink terminal sends a packet to Google?"**

You have now answered this through 9 labs. In this step, synthesize your knowledge into a comparative narrative with Mission 01.

**Step 2 — Build the side-by-side architecture comparison**

Using draw.io, create a dual-column diagram:

|Cellular (Mission 01)|Satellite (Mission 02)|
|---|---|
|User device|User device|
|SIM authentication (5G AKA)|Terminal authentication (STSAFE certificate)|
|Local IP assignment (DHCP)|Local IP assignment (DHCP via Starlink router)|
|5G NR radio (sub-6 GHz or mmWave)|Ku-band RF (~14 GHz uplink, ~11 GHz downlink)|
|Fixed gNodeB (cell tower)|Moving LEO satellite (~7.6 km/s)|
|Carrier core (SGW, PGW, HSS)|Constellation (ISL routing, beam switching)|
|Carrier edge (CG-NAT, firewall)|Gateway station (de-encryption, peering)|
|Internet backbone|Internet backbone|
|Destination server|Destination server|

Annotate similarities and differences:

- Both use IP, TCP, DNS, TLS (application layer is identical)
- Cellular: infrastructure is fixed; Satellite: infrastructure moves constantly
- Cellular: handover when user moves; Satellite: handover every few minutes
- Cellular: carrier owns everything; Satellite: SpaceX owns satellites + gateways, customer owns terminal

**Step 3 — Create the protocol stack comparison**

|Layer|Cellular (5G)|Satellite (Starlink)|Notes|
|---|---|---|---|
|Application|HTTP/HTTPS, QUIC|HTTP/HTTPS, QUIC|Identical|
|Transport|TCP/UDP|TCP/UDP|Identical|
|Network|IP|IP|Identical|
|Link|5G protocol (encrypted)|Proprietary (AES-256 encrypted)|Different protocols, similar encryption goals|
|Physical|5G NR (radio)|Ku-band RF (phased array)|Different frequencies, both wireless|

Key finding: The **lower layers differ fundamentally**, but once IP traffic reaches the gateway/carrier core, the architectures converge. End-to-end security (TLS) is the same in both cases.

**Step 4 — Map attack surfaces side-by-side**

|Attack Vector|Cellular (Mission 01)|Satellite (Mission 02)|Comparative Risk|
|---|---|---|---|
|RF eavesdropping|Possible (5G encryption)|Possible (AES-256 encryption)|Similar (both encrypted)|
|RF jamming|Possible (cell tower range)|Possible (larger coverage area, weaker signals)|Higher for satellite|
|Physical access to infrastructure|Cell tower accessible|Gateway fenced; satellite inaccessible|Lower for satellite|
|Insider threat|Carrier employee|SpaceX employee|Similar|
|Terminal compromise|Phone malware|Firmware bypass (mod chip)|Similar (hardware trust boundary)|
|Backhaul cut|Fiber to tower|Fiber to gateway|Similar (both use fiber)|
|Routing manipulation|BGP hijack|BGP hijack|Identical (Internet is shared)|
|Weather impact|Minimal|Moderate (rain fade)|Higher for satellite|
|Power loss|Phone has battery|Terminal has NO battery|Higher for satellite|
|Handover gap|Only when moving|Every few minutes|Higher for satellite|
|Supply chain|Phone manufacturer|Terminal manufacturer|Similar|
|Nation-state attack|IMSI catcher, tower compromise|ASAT, jamming, spoofing|Different capabilities|

**Step 5 — Compare availability and resilience**

|Factor|Cellular|Satellite|Winner|
|---|---|---|---|
|Latency (median)|~20-40 ms|~25-50 ms|Comparable (both excellent for LEO/fiber mix)|
|Latency (geostationary baseline)|N/A|~500-800 ms (would be worse if GEO)|Cellular wins vs. traditional satellite|
|Weather resilience|Excellent|Moderate (rain fade)|Cellular wins|
|Coverage area|Limited to tower density|Near-global (sky visible)|Satellite wins (remote areas)|
|Handover frequency|Low (only when moving)|High (every 4-10 minutes)|Cellular wins (fewer disruptions)|
|Power dependence|Phone has battery|Terminal needs wall power|Cellular wins|
|Single point of failure|Tower, backhaul|Gateway, terminal power|Comparable (both have weak points)|
|Disaster recovery|Depends on tower survival|Works if sky is clear (no fiber dependency to user)|Satellite wins (no ground infrastructure to user)|

**Step 6 — Compare security controls**

|Control Type|Cellular Implementation|Satellite Implementation|Equivalency|
|---|---|---|---|
|Encryption|5G encryption (SIM-based)|AES-256 link encryption|Similar strength|
|Authentication|SIM credential (AKA protocol)|Hardware certificate (STSAFE-A110)|Similar model (device identity)|
|Access control|Subscriber provisioning|Terminal provisioning|Similar (account-based)|
|Network monitoring|Carrier NOC analytics|SpaceX NOC analytics|Similar (operator-managed)|
|Physical security|Tower fencing, alarms|Gateway fencing, surveillance|Similar (infrastructure)|
|End-to-end security|TLS (user-controlled)|TLS (user-controlled)|Identical|

**Step 7 — Write the comparative narrative**

Produce the final narrative (3,000–5,000 words) structured as:

`# MISSION 02 FINAL EXPLANATION: SATELLITE → INTERNET → CELLULAR COMPARISON ## Introduction [One paragraph framing the satellite journey and why it differs from terrestrial] ## Section 1: Before the Request — Terminal Preparation - Terminal power state and initialization - GPS-assisted satellite acquisition - Certificate-based authentication (STSAFE-A110) - IP address assignment via Starlink router ## Section 2: RF Link — Ku-Band Uplink - Phased array beamforming (electronic, not mechanical) - AES-256 encryption applied at terminal - Signal transmission at ~14 GHz - Weather impact (rain fade considerations) ## Section 3: Space Segment — Constellation Routing - Satellite receives uplink, decrypts (at link layer only) - Optional ISL routing (laser links at 1064 nm) - Beam switching as satellite moves - Handover to next satellite ## Section 4: Downlink to Gateway - Satellite → Gateway Ka-band/E-band downlink - Gateway decrypts payload (link encryption terminates here) - Traffic enters plaintext IP routing ## Section 5: Internet Transit - Same as Mission 01 (BGP routing, IXPs, CDN) - TLS/HTTPS still required for end-to-end confidentiality - No special handling at peering points ## Section 6: Destination and Return Path - Google processes request (same as cellular) - Response follows reverse path (may take different route) - Terminal receives encrypted response, decrypts, forwards to device ## Section 7: Security Throughout Where confidentiality, integrity, and authentication are established at each layer, and where vulnerabilities exist. ### Comparison with Mission 01 Cellular - Shared security mechanisms (TLS, DNS, IP routing) - Divergent security mechanisms (RF link encryption, authentication methods) - Relative advantages and disadvantages ## Section 8: When to Use Each Architecture - Cellular: Urban/suburban, latency-sensitive, weather-resilient applications - Satellite: Remote/rural, maritime, disaster recovery, mobility beyond cellular coverage - Hybrid scenarios (backhaul for remote cell towers) ## Conclusion What makes satellite networking unique? Where does it overlap with terrestrial? What security properties are equivalent? What remains fundamentally different?`

**Step 8 — Create supporting diagrams**

1. **Dual-column journey diagram** (Cellular vs. Satellite side-by-side)
2. **Protocol stack overlay** (showing where layers match/differ)
3. **Attack surface heat map** (comparing relative risk by attack vector)
4. **Availability decision tree** (when to choose satellite vs. cellular)

**Step 9 — Self-assessment against Security+ coverage**

For each atomic requirement marked 🟢 in the Mission 02 Passport coverage table, verify evidence:

|Requirement|Does my evidence prove demonstration?|Gap or confidence issue|
|---|---|---|
|1.4-B Encryption|Yes — RF link encryption analysis, AES-256 documented|None|
|4.1-D Wireless security|Yes — comprehensive RF security investigation|None|
|2.2-H Attack surfaces|Yes — attack surface map for all components|None|
|...|...|...|

Adjust claims if evidence is weaker than stated.

**Step 10 — Reflection and gap analysis**

Address:

1. **Learning progression:** What did you understand about satellite networking at the start vs. the end?
2. **Comparative thinking:** How does understanding both cellular and satellite change your perspective on wireless security?
3. **Security posture:** Can you now identify where security fails in satellite systems vs. terrestrial systems?
4. **Evidence literacy:** What evidence is strong (measurable) vs. speculative (theoretical only)?
5. **Remaining gaps:** What Security+ topics still need work in later missions? (Governance, IAM, cloud, compliance)

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Side-by-side architecture diagram (draw.io)|Comparative journey reconstruction|
|Protocol stack comparison table|Part of comparative analysis|
|Attack surface heat map (draw.io)|Attack-surface map (comparative)|
|Availability decision tree (draw.io)|Part of technical report|
|Final comparative narrative (3,000–5,000 words)|Comparative journey reconstruction|
|Security+ coverage self-assessment|Security+ atomic coverage record|
|Reflection and gap analysis|Part of Mission 02 technical report|

### Success Criteria

- Dual-column diagrams clearly show architectural parallels and divergences
- Protocol stack comparison accurately identifies matching and differing layers
- Attack surface heat map ranks relative risk for shared and unique threats
- Narrative explains when to use satellite vs. cellular based on security and performance
- Self-assessment honestly identifies weak evidence areas
- Learner can explain the complete satellite journey without reading from notes

### Curiosity Branches (for Future Missions)

- How would Mission 07 (Cloud Migration) connect to satellite infrastructure (space-as-a-service)?
- How would Mission 04 (Network Compromised) apply a satellite link compromise scenario?
- What happens when a ship's Starlink terminal is used while in international waters (jurisdictional questions)?
- How does Amazon's Project Kuiper architecture compare to Starlink's?