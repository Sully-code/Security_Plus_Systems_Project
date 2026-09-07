## LAB 01 — Satellite Architecture Research

### Objective

Research and document the complete Starlink LEO constellation architecture across all zoom levels. Produce multi-level system diagrams that accurately represent the user terminal, space segment, and ground infrastructure. This establishes the conceptual model for all subsequent labs.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|3.1-A|On-premises architecture|🟡 Understood|Satellite terminal as customer-premises equipment documented|
|3.1-B|Cloud architecture|🟡 Understood|Distributed constellation parallels to cloud infrastructure documented|
|3.2-A|Infrastructure considerations|🟢 Demonstrated|Multi-level architecture diagrams with physical site considerations|
|2.2-H|Attack surfaces|🟢 Demonstrated|Every architectural component annotated as potential attack surface|

### Prerequisites

Mission 01 complete. Understanding of layered network architecture from Labs 01–02.

### Tools

- Web browser (research)
- draw.io
- Starlink public resources: starlink.com/technology, starlink.com/updates
- starlink.sx (public constellation tracker)
- FCC filing database (public)

### Procedure

**Step 1 — Research the constellation architecture**

Using the sources below, gather facts about each architectural layer. Document every claim with a citation.

Key sources (all free):

- starlink.com/technology — official technical overview
- starlink.com/public-files/starlinkProgressReport_2025.pdf — progress report
- en.wikipedia.org/wiki/Starlink — curated summary with extensive citations
- eoportal.org/satellite-missions/starlink — detailed spacecraft specifications
- starlink.sx — real-time satellite positions

Research and document answers to these questions:

**User Terminal (CPE):**

- What hardware comprises a Starlink user terminal? (dish, router, power supply, cables)
- What frequency bands does the user terminal use? (Document the specific GHz ranges)
- How does the phased array antenna steer beams without moving parts?
- What role does the STSAFE-A110 security chip play?

**Space Segment:**

- How many satellites are currently operational? (Record the number and date of your research)
- What orbital altitudes are used? (Document multiple shells if present)
- How many inter-satellite laser links does each satellite carry?
- What bandwidth do the laser links achieve?
- What is the approximate orbital period at ~550 km?

**Ground Infrastructure:**

- Approximately how many gateway stations exist worldwide?
- What frequency bands do gateways use? (Different from user terminals)
- How are gateways connected to the Internet backbone?
- What physical protections are typically present at gateway sites?

**Step 2 — Create Level 0 diagram (User View)**

In draw.io, create the simplest representation:

`USER DEVICE → STARLINK TERMINAL → INTERNET → WEBSITE`

Annotate with: "What the user sees and interacts with."

**Step 3 — Create Level 1 diagram (Major System View)**

Expand to show major architectural blocks:

`USER DEVICE ↓ (Wi-Fi/Ethernet) STARLINK ROUTER (CPE) ↓ PHASED ARRAY ANTENNA (DISH) ↓ (Ku-band RF uplink) LEO SATELLITE ↓ (optional: inter-satellite laser link) GATEWAY GROUND STATION ↓ (fiber backhaul) INTERNET POINT OF PRESENCE ↓ DESTINATION SERVER`

Label each block with its real-world function. Add the specific frequency bands and protocols at each boundary.

**Step 4 — Create Level 2 diagram (Constellation View)**

Show the space segment in detail:

`┌─────────────────────────────────────────────────┐ │ LEO CONSTELLATION │ │ │ │ Sat A ←─laser─→ Sat B ←─laser─→ Sat C │ │ ↑ ↑ ↑ │ │ User link (relay) Gateway │ │ link │ └──────┬──────────────────┬────────────────┬──────┘ ↓ ↓ ↓ USER TERMINAL (no ground GATEWAY station STATION needed)`

Document:

- Why LEO (~550 km) instead of GEO (~35,786 km)? Calculate the speed-of-light round-trip time for each.
- How many satellites are typically visible from one location?
- What happens during satellite handover?

**Step 5 — Create Level 3 diagram (Protocol/Communication View)**

Map the protocol stack at each major boundary:

|Layer|User Terminal → Satellite|Satellite → Gateway|Gateway → Internet|
|---|---|---|---|
|Application|HTTP/HTTPS|HTTP/HTTPS|HTTP/HTTPS|
|Transport|TCP/QUIC|TCP/QUIC|TCP/QUIC|
|Network|IP|IP|IP|
|Link|Proprietary (encrypted)|Proprietary (encrypted)|Ethernet/fiber|
|Physical|Ku-band RF|Ka-band RF|Fiber optic|

Note where encryption is applied and where it terminates.

**Step 6 — Annotate attack surfaces**

On each diagram, mark every component as a potential attack surface:

- User terminal (physical access, firmware tampering)
- Wi-Fi link (if not secured)
- Ku-band RF link (interception, jamming, spoofing)
- Satellite onboard processing (command intrusion)
- Inter-satellite laser link (interception theoretically possible but extremely difficult)
- Gateway ground station (physical attack, network intrusion)
- Fiber backhaul (physical cable cut, interception)
- Internet transit (BGP hijacking — same as Mission 01)

**Step 7 — Write the architecture summary**

Produce a 500–1,000 word document that explains the complete architecture in plain language. Structure it as:

1. What the user has at their location
2. How data gets from the terminal to a satellite
3. What happens inside the constellation
4. How data gets from satellite to the Internet
5. How the response gets back

Cite specific sources for every factual claim.

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Level 0 satellite system diagram|Level 0 diagram|
|Level 1 ground-space architecture|Level 1 architecture diagram|
|Level 2 constellation view|Level 2 architecture diagram|
|Protocol stack diagram|Protocol-stack diagram|
|Attack surface annotations|Attack-surface map|
|Architecture summary document|Part of Mission 02 technical report|

### Success Criteria

- All four diagram levels are produced with accurate labels
- Frequency bands, orbital altitudes, and satellite counts are cited to sources
- Attack surfaces are annotated on every diagram
- Architecture summary could be understood by someone without prior satellite knowledge
- Learner can answer: "What happens when my Starlink terminal sends a packet to Google?" at a high level

### Curiosity Branches

- How does a phased array antenna steer a beam electronically without moving?
- What is the difference between Ku-band and Ka-band in terms of rain fade?
- How does GPS/GNSS help the terminal find satellites?
- What happens to old satellites at end-of-life? (Research the FCC 5-year deorbit rule)