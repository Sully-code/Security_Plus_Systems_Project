## LAB 05 — Availability Analysis

### Objective

Research and document the availability characteristics of the Starlink system. Understand redundancy mechanisms, measure expected uptime, analyze latency behavior, and compare availability to terrestrial alternatives.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|3.4-A|High availability|🟢 Demonstrated|Redundant gateway, multi-satellite visibility, handover analysis|
|3.4-B|Site considerations|🟢 Demonstrated|Geographic gateway distribution, site selection criteria|
|3.4-C|Resilience testing|🟢 Demonstrated|Failure scenario analysis with recovery mechanisms|
|3.4-D|Power considerations|🟢 Demonstrated|Backup power at gateways, terminal power dependencies|
|3.4-G|Continuity of operations|🟡 Understood|Disaster scenario discussion|
|1.2-C|Availability|🟢 Demonstrated|Availability as CIA triad component analyzed|
|1.1-I|Compensating controls|🟡 Understood|Alternative routing when primary path fails|

### Prerequisites

Lab 01 complete. Mission 01 Lab 06 (Routing Failure) complete for comparison.

### Tools

- Web browser (research)
- draw.io
- Python 3 (for latency calculations)
- Ookla Speedtest public reports

### Procedure

**Step 1 — Document redundancy mechanisms**

Research and map every redundancy layer in the Starlink architecture:

|Layer|Redundancy Mechanism|Failover Time|Evidence Source|
|---|---|---|---|
|Satellite visibility|Multiple satellites in view from any location|Seconds (handover)|Orbital mechanics, constellation size|
|Gateway stations|~150-170 gateways worldwide; traffic reroute|Minutes|SpaceX progress reports|
|Inter-satellite links|Mesh routing — traffic can take multiple paths|Seconds|Laser ISL architecture|
|Internet PoPs|Multiple peering points|Seconds-minutes|Network architecture|
|Power (gateway)|UPS + generator backup|Immediate (UPS), hours (generator)|Standard datacenter practice|
|Power (terminal)|Customer-provided; no built-in battery|N/A — terminal dies|Terminal spec sheet|
|Fiber backhaul|Redundant paths to IXPs|Seconds (if BGP reconverges)|Network design|

**Step 2 — Calculate availability expectations**

Using Starlink's published data and Ookla reports:

Published performance (as of 2025–2026):

- Median peak-hour latency: ~25.7 ms (US)
- Fewer than 1% of measurements exceed 55 ms latency
- Median download: ~200 Mbps (peak demand, US)
- Active satellites: ~10,000+
- Active customers: millions

Calculate:

1. **Theoretical availability:** If satellites pass overhead every ~4 minutes and handover takes ~seconds, what percentage of time should service be uninterrupted?
2. **Weather availability:** If rain fade causes 2% downtime in heavy-rain regions, what is the effective availability? (Express as nines: 99.9%, 99.99%, etc.)
3. **Gateway redundancy:** If the nearest gateway goes offline and traffic reroutes to one 500 km farther, what is the latency penalty?

**Step 3 — Model the handover process**

In draw.io, create a timeline diagram showing satellite handover:

`Time → T+0 T+2min T+4min T+6min │ │ │ │ SAT A visible ──── handover ── SAT B visible ──── handover ── SAT C │ │ │ │ ▼ ▼ ▼ ▼ Connected Brief gap Connected Brief gap (low lat) (<1 sec?) (low lat) (<1 sec?)`

Document:

- How long is a satellite visible from one location? (Calculate from orbital velocity at ~550 km altitude and minimum elevation angle)
- What happens during handover? (Does TCP notice? Does the terminal maintain session state?)
- How does this compare to cellular handover in Mission 01?

**Step 4 — Analyze power dependencies**

Document the power architecture:

**Gateway stations:**

- Primary: Grid power
- Secondary: UPS (uninterruptible power supply) — battery backup for immediate failover
- Tertiary: Diesel/gas generator — extended outage coverage
- Typical runtime: 24-72 hours on generator (estimated; varies by site)

**User terminal:**

- Power: 50-75W during operation
- No built-in battery — terminal dies immediately on power loss
- Customer must provide UPS or generator for resilience

**Satellites:**

- Power: Solar panels + onboard batteries
- Batteries sustain operation during eclipse (Earth shadow)
- Eclipse duration at ~550 km: ~35 minutes per orbit

Answer: What is the weakest power resilience link in the system? (Hint: It's the user terminal.)

**Step 5 — Create the availability model**

In draw.io, create an availability flowchart:

`USER REQUEST ↓ Is a satellite visible? ─── No ──→ Wait/queue (seconds) ↓ Yes Is weather clear? ─── No ──→ Rain fade mitigation (power boost, alternate freq) ↓ Yes ↓ Is gateway online? ─── No ──→ Reroute to alternate gateway ↓ Yes ↓ Is fiber backhaul up? ─── No ──→ Reroute via ISL to another gateway ↓ Yes ↓ SERVICE DELIVERED DEGRADED SERVICE`

Document the availability formula:

- Overall availability = P(satellite visible) × P(weather clear enough) × P(gateway online) × P(backhaul up) × P(power available)

**Step 6 — Compare availability to terrestrial**

|Metric|Cellular (Mission 01)|Starlink (Mission 02)|Fiber Broadband|
|---|---|---|---|
|Typical uptime|99.9%+ (tower)|?|99.99%+|
|Weather impact|Minimal|Moderate (rain fade)|Minimal|
|Power dependency|Tower has backup|Terminal has NO backup|ONT needs power|
|Handover frequency|Only when moving|Every few minutes|Never (fixed)|
|Single points of failure|Cell tower, backhaul fiber|Terminal power, gateway|Fiber cut, ISP equipment|

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Redundancy mechanism table|Availability performance report|
|Availability calculations|Part of technical report|
|Satellite handover timeline diagram (draw.io)|Part of availability report|
|Power architecture analysis|Part of technical report|
|Availability flowchart (draw.io)|Part of availability report|
|Comparative availability table|Part of technical report|

### Success Criteria

- All redundancy layers are documented with failover times
- Availability calculations are mathematically sound
- Learner can explain why user terminal power is the weakest resilience link
- Handover process is compared to Mission 01 cellular handover
- Availability comparison includes at least three infrastructure types

### Curiosity Branches

- What is "rain fade" and why does it affect Ku/Ka-band more than cellular frequencies?
- How would you design a UPS system for a remote Starlink terminal?
- What is the Kessler Syndrome and how could it affect long-term availability?
- How do maritime Starlink terminals handle constant motion?