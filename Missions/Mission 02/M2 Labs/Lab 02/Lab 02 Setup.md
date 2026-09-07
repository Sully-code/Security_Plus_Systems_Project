## LAB 02 — Terrestrial vs. Satellite Comparison

### Objective

Systematically compare Starlink satellite networking to the terrestrial cellular networking studied in Mission 01. Document the tradeoffs in latency, reliability, security, cost, and architecture. This builds comparative systems thinking — a core Passport competency.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|1.2-C|Availability|🟢 Demonstrated|Redundancy comparison, handover analysis, failure mode comparison|
|3.4-A|High availability|🟢 Demonstrated|HA mechanisms in both architectures compared|
|3.4-E|Platform diversity|🟡 Understood|Satellite as alternative platform to terrestrial|
|2.5-E|Isolation|🟢 Demonstrated|Network isolation approaches compared|
|3.2-A|Infrastructure considerations|🟢 Demonstrated|Physical infrastructure requirements contrasted|

### Prerequisites

Lab 01 complete. Mission 01 Labs 01–02 complete (terrestrial architecture).

### Tools

- Mission 01 architecture diagrams (from your archive)
- Mission 02 Lab 01 architecture diagrams
- draw.io
- Web browser (for performance benchmark research)
- Ookla Speedtest public reports (ookla.com/articles)

### Procedure

**Step 1 — Build the comparison framework**

Create a master comparison table with these dimensions:

|Dimension|Mission 01 (Cellular/Terrestrial)|Mission 02 (Satellite/LEO)|
|---|---|---|
|Last-mile medium|Cellular radio (5G NR)|Ku-band satellite RF|
|Distance to first hop|~1–5 km (cell tower)|~550 km (LEO satellite)|
|Theoretical minimum latency|?|?|
|Observed median latency|?|?|
|Number of moving infrastructure nodes|Fixed (towers don't move)|Moving (satellites orbit at ~7.6 km/s)|
|Handover frequency|Only when user moves between cells|Constant — satellites pass overhead every few minutes|
|Infrastructure ownership|Carrier owns towers, core|SpaceX owns satellites, gateways, terminals|
|Encryption at link layer|5G encryption (SIM-based)|RF link encryption (AES-256, hardware key)|
|Physical security of infrastructure|Towers fenced, alarmed|Ground stations fenced; satellites physically inaccessible|
|Weather impact|Minimal (5G is robust)|Significant (rain fade at Ku/Ka-band)|
|Geographic coverage|Limited to tower coverage area|Near-global (wherever sky is visible)|
|Redundancy model|Multiple towers in range|Multiple satellites in view, multiple gateways|
|Attack surface|RF interception, tower access, core network|RF interception, jamming, terminal tampering, ground station access|
|Cost to deploy|Per-tower infrastructure|Per-satellite launch cost (amortized)|

**Step 2 — Calculate and compare theoretical latencies**

Use the speed of light (~3×10⁸ m/s) to calculate minimum round-trip times:

**Cellular (Mission 01):**

- Phone to tower: ~1–5 km
- Tower to carrier core: ~10–50 km (fiber)
- Minimum RTT contribution from distance: ?

**Satellite (Mission 02):**

- Terminal to satellite: ~550 km (straight up)
- Satellite to gateway: ~550 km (down)
- Potential inter-satellite hop: variable
- Minimum RTT contribution from distance: ?

**GEO satellite (for context):**

- Terminal to satellite: ~35,786 km
- What would the minimum RTT be?

Document your calculations. Explain why LEO satellite latency is dramatically lower than GEO despite both being "satellite."

**Step 3 — Research observed performance data**

Using free public sources:

- Ookla satellite broadband reports (ookla.com/articles)
- Starlink's own network updates (starlink.com/updates)
- Reddit r/Starlink community speed test aggregations (qualitative only)

Document:

- Median Starlink latency in the US (as of most recent data you can find)
- Median terrestrial broadband latency for comparison
- How often latency spikes occur and why
- Download/upload speed comparisons

**Step 4 — Create the comparison diagram**

In draw.io, create a side-by-side architectural comparison:

Left column: Mission 01 journey (Phone → Tower → Carrier → Internet → Google) Right column: Mission 02 journey (Laptop → Starlink terminal → Satellite → Gateway → Internet → Google)

Annotate:

- Where the journeys are architecturally similar (both use IP, TCP, TLS, DNS)
- Where they fundamentally diverge (RF medium, mobility of infrastructure, handover triggers)
- Where trust boundaries exist in each model

**Step 5 — Analyze isolation and segmentation differences**

Document how each architecture isolates users:

**Cellular:**

- Each subscriber gets a private IP behind CG-NAT
- GTP tunnels isolate user traffic in the core
- VLANs in the transport network

**Satellite:**

- Each terminal authenticated via certificate (STSAFE-A110)
- Link-layer encryption isolates terminal traffic on the RF link
- How is traffic isolated between the satellite and gateway?
- What happens if a satellite processes traffic from multiple terminals?

Answer: Which architecture provides stronger isolation? Why? What are the tradeoffs?

**Step 6 — Document the resilience comparison**

Create a failure-mode comparison table:

|Failure Scenario|Cellular Impact|Satellite Impact|Recovery Mechanism|
|---|---|---|---|
|Tower/satellite goes offline|Lose service until another tower is in range|Handover to next satellite (seconds)|Automatic|
|Severe weather|Minimal|Rain fade may degrade or drop link|Power adaptation, alternate frequencies|
|Power outage at infrastructure site|Tower battery backup (hours)|Gateway has backup power; satellite is solar-powered|Battery/generator|
|Physical infrastructure attack|Tower accessible, can be climbed/cut|Ground station fenced; satellite unreachable|Physical security|
|Backhaul cut|Fiber to tower cut = tower offline|Fiber to gateway cut = gateway offline (traffic rerouted)|Multiple gateways|
|Regulatory shutdown|Carrier license revoked|Spectrum license revoked (FCC/ITU)|Legal/regulatory|

**Step 7 — Write the comparison analysis**

Produce a 1,000-word analysis answering:

1. When is satellite networking superior to terrestrial? (Remote areas, maritime, disaster recovery)
2. When is terrestrial superior? (Urban density, latency-sensitive applications, weather resilience)
3. What security properties are equivalent between the two? (TLS, DNS, IP routing)
4. What security properties differ? (Link-layer encryption, physical access to infrastructure)
5. How does infrastructure mobility (moving satellites) change the security model?

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Master comparison table|Terrestrial vs. satellite comparison|
|Latency calculation worksheet|Part of technical report|
|Side-by-side architecture diagram (draw.io)|Comparative architecture diagram|
|Failure-mode comparison table|Part of technical report|
|Comparison analysis document|Terrestrial vs. satellite comparison|

### Success Criteria

- Comparison table is populated with cited data for every cell
- Latency calculations are mathematically correct
- Side-by-side diagram clearly shows architectural parallels and divergences
- Learner can articulate when satellite is preferable to terrestrial and vice versa
- Isolation and segmentation differences are explained with Security+ terminology

### Curiosity Branches

- What would a hybrid architecture look like? (Starlink backhaul for a remote cellular tower)
- How does TCP behave differently over satellite links? (Research TCP performance over high-bandwidth-delay-product links)
- Could a Starlink terminal replace a corporate VPN? What would be gained/lost?