## LAB 04 — Physical Security Assessment

### Objective

Assess the physical security of satellite ground infrastructure using only public data. Identify what physical attack surfaces exist at ground stations, user terminal sites, and for the satellites themselves. This lab develops physical security thinking — a Security+ domain often neglected in network-focused curricula.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|1.1-G|Physical controls|🟢 Demonstrated|Ground station physical security assessment documented|
|2.4-D|Physical attacks|🟢 Demonstrated|Physical attack vectors catalogued with mitigations|
|3.2-B|Control selection|🟢 Demonstrated|Physical security controls justified for each infrastructure type|
|1.1-D|Deterrent controls|🟡 Understood|Signage, fencing as deterrents discussed|
|2.1-D|Insider threats|🟡 Understood|Ground station personnel as potential insider threat|
|2.2-F|Supply chain vectors|🟡 Understood|Terminal hardware provenance concerns|

### Prerequisites

Lab 01 complete (architecture understanding).

### Tools

- Web browser (research)
- draw.io
- Google Maps / Google Earth (free, for satellite imagery of known gateway sites)

### Procedure

**Step 1 — Research gateway station physical security**

Using public sources:

- Reddit discussions with photos of Starlink gateway sites
- YouTube tours of gateway stations (e.g., the Prosser, WA site tour)
- FCC earth-station filings (contain coordinates and site descriptions)
- starlink.sx gateway location map

Document the typical physical security controls at a gateway station:

|Control Type|Implementation|Purpose|
|---|---|---|
|Perimeter fencing|Chain-link with barbed wire topping|Deter unauthorized entry|
|Locks|High-security padlocks|Prevent casual entry|
|Surveillance|CCTV cameras|Detective control, evidence collection|
|Location|Remote/rural areas|Reduce casual encounters|
|Radomes|Weather-protected antenna enclosures|Environmental protection, not security|
|Lighting|Site lighting|Deter nighttime entry|
|Access control|Locked gates, key management|Restrict to authorized personnel|

**Step 2 — Map a known gateway site**

Using Google Maps/Earth and the coordinates from FCC filings or community maps:

1. Find a known Starlink gateway location (e.g., Prosser, WA — well-documented)
2. Examine the satellite imagery
3. Identify visible security features (fencing, buildings, antenna arrays)
4. Document what you can observe from public imagery alone

In draw.io, create a site layout diagram showing:

- Antenna positions (the radomes)
- Fenced perimeter
- Access roads
- Buildings (equipment, NOC)
- Power infrastructure (if visible)
- Nearest road and population center

**Step 3 — Assess physical attack surfaces**

For each infrastructure component, document the physical threat:

**3a. User Terminal (Customer Site):**

- Attack: Physical theft or tampering with the dish
- Impact: Terminal could be modified (fault injection), stolen for key extraction, or relocated
- Mitigation: Secure mounting, tamper-evident seals (if implemented), remote deactivation by network
- Residual risk: Customer sites have the weakest physical security

**3b. Gateway Station:**

- Attack: Forced entry, vandalism, cable cutting at perimeter
- Impact: Loss of gateway capacity, traffic rerouting to alternate gateways
- Mitigation: Fencing, locks, surveillance, remote locations
- Residual risk: Determined attackers could breach perimeter; insider threat is significant

**3c. Satellite (On-Orbit):**

- Attack: Anti-satellite weapons (ASAT), laser dazzling, grappling
- Impact: Permanent loss of satellite capacity; debris generation
- Mitigation: Physically inaccessible to most actors; orbital maneuverability
- Residual risk: Nation-state actors with ASAT capability; debris cascade (Kessler Syndrome)

**3d. Fiber Backhaul:**

- Attack: Cable cut between gateway and Internet PoP
- Impact: Gateway isolated; traffic rerouted (if alternate paths exist)
- Mitigation: Redundant fiber paths, buried cables
- Residual risk: Construction accidents, deliberate cable cuts

**3e. Power Infrastructure:**

- Attack: Cut power to gateway or terminal
- Impact: Service outage
- Mitigation: Backup generators, UPS, battery backup
- Residual risk: Extended outages exceeding backup capacity

**Step 4 — Create the physical security assessment matrix**

|Asset|Threat|Likelihood|Impact|Current Controls|Gap|
|---|---|---|---|---|---|
|User terminal|Theft/tampering|Medium|Medium|Mounting, remote deactivation|Limited physical hardening|
|Gateway station|Forced entry|Low|High|Fencing, locks, CCTV|No armed security (typically)|
|Satellite|ASAT/debris|Very Low|Critical|Inaccessible location, maneuverability|No defense against kinetic ASAT|
|Fiber backhaul|Cable cut|Low|High|Redundant paths, burial|Single points may exist|
|Power supply|Outage|Medium|High|UPS, generator backup|Fuel-limited runtime|

**Step 5 — Analyze insider threat at ground stations**

Document:

- Who has physical access to gateway stations? (Site technicians, SpaceX employees, potentially contractors)
- What could an insider do? (Connect to internal networks, modify antenna configurations, install monitoring equipment)
- How does this compare to Mission 01's carrier insider threat?
- What controls mitigate insider risk? (Background checks, access logging, job rotation, dual control)

**Step 6 — Document supply chain concerns**

Research and document:

- Where are Starlink terminals manufactured? (SpaceX facilities in Redmond, WA and Bastrop, TX)
- What supply chain risks exist? (Counterfeit components, firmware tampering during manufacture, intercepted shipments)
- How does the STSAFE-A110 chip address supply chain risk? (Keys provisioned at manufacture, hardware-fused)
- What can't the security chip prevent? (Physical side-channel attacks, fault injection as demonstrated by Wouters)

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Gateway physical security assessment|Physical security assessment|
|Site layout diagram (draw.io)|Part of physical security assessment|
|Physical attack surface analysis (5 asset types)|Part of technical report|
|Physical security assessment matrix|Physical security assessment|
|Insider threat analysis|Part of technical report|
|Supply chain risk analysis|Part of technical report|

### Success Criteria

- At least one gateway site is analyzed using public imagery
- Five physical attack surfaces are documented with likelihood, impact, and controls
- Learner can explain why user terminals are the weakest physical security link
- Insider threat analysis considers both gateway and network operations personnel
- Supply chain analysis connects to Security+ 2.2-F and 2.3-H

### Curiosity Branches

- What is the Kessler Syndrome and why does debris matter for LEO constellations?
- How do military satellite ground stations differ from commercial ones in physical security?
- What is TEMPEST and does it apply to satellite ground stations?
- How would you design physical security for a gateway station in a hostile environment?