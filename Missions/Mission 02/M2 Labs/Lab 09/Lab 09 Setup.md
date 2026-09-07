# LAB 09 — REGULATORY ANALYSIS

### Objective

Research the regulatory landscape governing satellite communications. Understand spectrum licensing, orbital slot allocation, debris mitigation rules, international coordination, and compliance requirements. This lab connects technical architecture to governance — a Security+ Domain 5 topic.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|5.1-E|External considerations|🟡 Understood|Spectrum regulation, international law, compliance|
|3.2-A|Infrastructure considerations|🟢 Demonstrated|Regulatory constraints on infrastructure deployment|
|5.2-G|Risk strategies|🟡 Understood|Compliance as risk mitigation strategy|
|5.4-D|Privacy|🟡 Understood|Traffic handling and surveillance law implications|

### Prerequisites

Lab 01 complete. Understanding of FCC/ITU roles.

### Tools

- Web browser (research)
- Markdown/text editor
- draw.io (for regulatory flowchart)

### Procedure

**Step 1 — Research the regulatory framework**

Document the multi-layer regulatory structure:

|Layer|Organization|Role|Scope|
|---|---|---|---|
|National (US)|FCC (Federal Communications Commission)|Spectrum licensing, orbital debris rules, market authorization|US territory, US companies|
|National (US)|FAA (Federal Aviation Administration)|Launch licensing, re-entry safety|Launch vehicles|
|National (US)|NOAA|Remote sensing licensing|Imaging satellites|
|International|ITU (International Telecommunication Union)|Spectrum coordination, orbital slot registration|Global coordination|
|International|UN COPUOS|Debris mitigation guidelines, space law|International norms|
|Inter-agency|IADC (Inter-Agency Space Debris Coordination Committee)|Debris mitigation standards|Space agencies|

Sources: FCC Part 25 (47 CFR Part 25), ITU Radio Regulations, FCC satellite licensing guides, Orbital Radar "Who Regulates Space?"

**Step 2 — Document the FCC licensing process**

Research and document the requirements for launching a commercial LEO constellation:

From 47 CFR Part 25 and FCC filings:

1. **Application submission:**
    
    - Submit through FCC's IBFS (International Bureau Filing System)
    - File Schedule S with orbital parameters, frequency assignments, power levels
    - Provide interference analysis
    - Submit draft ITU filing materials
2. **Technical review:**
    
    - FCC reviews against Part 25 rules (Subparts B and C)
    - Coordinates with other operators in same frequency bands
    - Assesses compatibility with existing services
3. **Debris mitigation:**
    
    - Submit orbital debris mitigation plan
    - Demonstrate post-mission disposal within 5 years (new 2022 rule)
    - Show probability of accidental breakup is minimized
4. **License grant:**
    
    - Conditional approval
    - License valid for 10 years (typical)
    - Performance milestones required

**Step 3 — Research the 5-year deorbit rule**

Key change: FCC adopted September 2022, effective for new applications after September 29, 2024:

- OLD: 25-year guideline (NASA/IADC standard carried over)
- NEW: 5-year mandatory post-mission disposal

Document:

- Why did the FCC change the rule? (Orbital congestion, collision risk)
- How does Starlink comply? (Propulsion system for deorbit, passivation)
- What happens if a satellite cannot deorbit? (Debris becomes permanent hazard)

**Step 4 — Document ITU coordination process**

The ITU is NOT a licensing agency — it's a coordination body:

|Process|What Happens|Timeline|
|---|---|---|
|Advance Publication|Notify ITU of planned frequency/orbit use|Years before launch|
|Coordination|Coordinate with other operators using same frequencies|Variable|
|Notification|Formal request to record frequency assignment|After coordination|
|Recording|Entry in Master International Frequency Register|Ongoing|

Why does ITU coordination matter?

- Prevents harmful interference between systems
- Establishes "first-come, first-served" priority (in practice)
- Countries can reject non-coordinated systems

**Step 5 — Analyze spectrum sharing rules**

Starlink uses shared spectrum bands:

- Ku-band (10.7-12.7 GHz downlink, 14-14.5 GHz uplink)
- Ka-band (17.7-21.2 GHz downlink, 27.5-31 GHz uplink)
- V-band (40 GHz range, newer Gen2)
- E-band (71-86 GHz for feeder links)

Document:

- Why are these bands shared? (Limited spectrum available)
- What are the sharing limits? (Power-flux-density constraints, coordination requirements)
- What happens when another system causes interference? (Coordination, technical adjustments)

**Step 6 — Create the regulatory compliance flowchart**

In draw.io, create a flowchart showing the compliance pathway:

`COMPANY PLANNES SATELLITE CONSTELLATION ↓ Design system (frequencies, orbits, power levels) ↓ Submit FCC application (Schedule S, debris plan, ITU draft) ↓ FCC technical review (interference analysis, Part 25 rules) ↓ FCC grants conditional license ↓ File with ITU (advance publication → coordination → notification → recording) ↓ Launch satellites (FAA launch license, insurance) ↓ Operate service (ongoing compliance, reporting) ↓ End-of-life (deorbit within 5 years, passivation) ↓ License renewal/expiry`

Annotate with:

- Where security concerns might arise (e.g., export controls, foreign ownership restrictions)
- Where spectrum rights are established
- Where debris mitigation is enforced

**Step 7 — Research foreign ownership restrictions**

Document:

- Who can own a US satellite company? (US citizens, or foreign ownership capped at certain percentages)
- What approval is needed for foreign investment? (FCC + interagency review)
- Why does this matter for security? (Foreign influence, data access, sanctions)

**Step 8 — Document jurisdictional considerations**

When Starlink serves a customer in Country X:

1. Starlink needs FCC license (US company)
2. Starlink needs ITU coordination (international)
3. Customer's country may require its own license
4. Customer's country may restrict Starlink use (India example in early 2026)
5. Traffic from that customer may be subject to local surveillance laws

Create a table:

|Country|Status|Concern|
|---|---|---|
|US|Licensed (full authorization)|Standard FCC oversight|
|Ukraine|Emergency authorization during conflict|Potential use by adversaries|
|India|Delayed (pending security clearance, early 2026)|National security review|
|Vietnam|Approved (Feb 2026, 4 gateways planned)|Standard licensing|
|Australia|Licensed|Standard oversight|
|[Other countries]|Varies|Local law compliance|

**Step 9 — Write the regulatory analysis**

Produce a 1,000-word analysis covering:

1. **Why regulation exists:** Spectral scarcity, collision prevention, sovereignty, national security
    
2. **How regulation affects security:**
    
    - Licensing ensures operator accountability
    - Debris rules prevent long-term hazards
    - Foreign ownership restrictions protect against coercion
    - Spectrum coordination prevents interference (which could mask attacks)
3. **What happens when regulation fails:**
    
    - Non-compliant operators flood the spectrum
    - Debris cascades (Kessler Syndrome)
    - Rogue terminals operate without authentication
    - National security vulnerabilities (use of Starlink in conflicts)
4. **Compliance as a security control:**
    
    - Background checks on personnel (insider threat mitigation)
    - Export controls on technology (supply chain security)
    - Data handling laws (privacy protection)
5. **Remaining regulatory gaps:**
    
    - Enforcement difficulty (who monitors space?)
    - Jurisdictional conflicts (satellites cross borders constantly)
    - Pace of innovation (rules lag behind technology)

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Regulatory framework table|Regulatory landscape overview|
|FCC licensing process documentation|Part of technical report|
|5-year deorbit rule analysis|Part of technical report|
|ITU coordination flowchart|Regulatory landscape overview|
|Spectrum sharing documentation|Part of technical report|
|Jurisdictional status table|Part of technical report|
|Regulatory analysis document|Regulatory landscape overview|

### Success Criteria

- Multi-layer regulatory structure is documented (FCC, FAA, ITU, UN)
- FCC licensing process is mapped step-by-step
- 5-year deorbit rule is explained with rationale
- ITU coordination is distinguished from national licensing
- Spectrum sharing rules are documented with specific bands
- Jurisdictional table includes at least 5 countries with statuses
- Analysis connects regulation to security outcomes

### Curiosity Branches

- What is the Outer Space Treaty (1967) and what does it say about liability?
- How does SpaceX navigate export controls (ITAR/EAR) for satellite components?
- What happens when two satellite operators claim the same orbital slot?
- Could a country ban Starlink within its borders? (Legal and practical implications)