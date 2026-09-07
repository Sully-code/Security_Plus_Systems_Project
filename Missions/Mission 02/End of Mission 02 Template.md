# TERMINAL → GOOGLE: SATELLITE NETWORKING JOURNEY & COMPARISON

---

## INTRODUCTION

When a user connects a laptop to a Starlink terminal at a remote location and types `https://www.google.com` into their browser, a page loads within seconds. Unlike the cellular journey explored in Mission 01, this path traverses space — bouncing off a satellite moving at 7.6 km/s in low Earth orbit before touching traditional Internet infrastructure.

This document explains what actually happens during that journey — not as abstract textbook concepts, but as a traceable sequence of events investigated through 10 laboratory exercises. Every claim below is backed by evidence: architecture diagrams from FCC filings, frequency analysis from public technical specifications, failure simulations in Packet Tracer, and performance data from Ookla and SpaceX's own progress reports.

Where this journey overlaps with Mission 01's cellular path, we note the convergence. Where it fundamentally diverges, we explain why. This is the capstone artifact of Mission 02 — proof that the learner can reason about satellite networking as a security system, not just a technology curiosity.

**Security+ Coverage:** This narrative demonstrates mastery of Domain 1 (General Security Concepts), Domain 2 (Threats & Mitigations), Domain 3 (Security Architecture — with emphasis on 3.4 Resilience and 4.1-D Wireless Security), Domain 4 (Security Operations), and elements of Domain 5 (Risk Analysis) at the level specified in the Mission 02 Passport.

---

## SECTION 1 — BEFORE THE REQUEST: TERMINAL PREPARATION

### Power State and Satellite Acquisition

Before the terminal can send any data, it must be powered, find a satellite, and authenticate to the network.

- **Terminal Hardware:** A Starlink user terminal consists of a flat-panel phased array antenna (the "dish"), a router (RTU — Router Terminal Unit), and a power supply. Unlike a smartphone, the terminal has no battery — power loss means immediate service loss.
- **GPS-Assisted Acquisition:** The terminal uses GPS/GNSS to determine its position and calculate which satellites are currently overhead. Unlike a cellular phone that searches for the nearest fixed tower, the Starlink terminal must predict which moving satellites are visible and electronically steer its beam toward them.
- **Phased Array Steering:** The antenna does not move mechanically. Instead, hundreds of small antenna elements adjust their phase relationships to form a directional beam pointed at the satellite — a process called beamforming. This allows rapid tracking as satellites cross the sky.

### Certificate-Based Authentication

Unlike a cellular phone which uses a SIM card for authentication via the 5G AKA protocol, the Starlink terminal authenticates using a hardware-based certificate:

- **STSAFE-A110 Security Chip:** Each terminal contains a dedicated security chip rated at Common Criteria EAL5+. This chip holds a cryptographically signed certificate that uniquely identifies the terminal.
- **Mutual Authentication:** When the terminal connects to a satellite, it presents its certificate. The network verifies the terminal's identity, and the terminal verifies the network — mutual authentication prevents rogue terminals and rogue satellites alike.
- **Hardware-Fused Keys:** Encryption keys are permanently fused into the terminal's main system-on-chip and the STSAFE-A110. This means keys cannot be extracted via software — though researchers have demonstrated hardware fault-injection attacks that bypass these protections (Wouters, KU Leuven, Black Hat 2022).

**Evidence:** Lab 01 researched the terminal architecture and documented the STSAFE-A110's role. Lab 03 analyzed the authentication model and compared it to Mission 01's SIM-based authentication. Lab 04 assessed the supply chain implications of hardware-fused keys.

**Security+ Connection (1.2-E Authentication):** Authentication occurs before any user data flows. The terminal cannot access the network without proving its identity via cryptographic certificate.

### IP Address Assignment

Once authenticated, the terminal receives an IP address:

- **Local Network:** The Starlink router assigns private IP addresses to connected devices via DHCP (same as any home router).
- **Public IP:** The terminal itself receives a public IP address from SpaceX's address pool — unlike cellular carriers that heavily use CG-NAT, Starlink terminals typically receive a publicly routable IP (though SpaceX also uses carrier-grade NAT in some regions).
- **DNS Configuration:** DNS resolver addresses are provided by the network, typically SpaceX-operated resolvers or third-party resolvers like Google (8.8.8.8).

**Evidence:** Lab 01 documented the IP assignment flow. Lab 07 analyzed what diagnostic data is available about the terminal's network state.

---

## SECTION 2 — RF LINK — KU-BAND UPLINK

### Frequency and Transmission

Once the terminal has authenticated and acquired a satellite, it transmits data over the Ku-band RF uplink:

- **Uplink Frequency:** ~14–14.5 GHz (Ku-band)
- **Downlink Frequency:** ~10.7–12.7 GHz (Ku-band)
- **Modulation:** Advanced modulation schemes (QAM) encode digital data onto radio waves
- **Antenna:** Phased array, electronically steered (no moving parts)

**Evidence:** Lab 03 documented the complete frequency landscape. Frequencies were cited from FCC filings and starlink.com/technology.

### AES-256 Link Encryption

All RF traffic between the terminal and the satellite is encrypted at the link layer:

- **Algorithm:** AES-256 symmetric encryption with mutual authentication
- **Key Material:** Keys are derived from the hardware-fused secrets and the terminal's certificate
- **Scope:** Encryption covers the entire RF segment — terminal to satellite and satellite to gateway

**Critical distinction from TLS:** This link-layer encryption protects against RF eavesdropping. But it is **not** end-to-end encryption. Once traffic reaches the gateway and enters the Internet backbone, it becomes plaintext IP — exactly like any other Internet traffic. HTTPS/TLS is still required on top for true end-to-end confidentiality.

**Evidence:** Lab 03 performed a detailed comparison between the RF link encryption model and Mission 01's TLS model. Lab 04 compared what an observer can see on the RF link vs. what they can see on a cellular link.

**Security+ Connection (1.2-A Confidentiality, 1.4-B Encryption):** Link-layer encryption provides confidentiality over the wireless segment. But the encryption terminates at the gateway — creating a trust boundary. The user must trust that SpaceX does not inspect plaintext traffic at the gateway. This is architecturally identical to trusting a cellular carrier not to inspect traffic at the carrier core.

### Weather Impact (Rain Fade)

Ku-band signals at ~12–14 GHz are susceptible to atmospheric absorption, particularly rain:

- **Rain Fade:** Heavy rain absorbs and scatters RF energy at these frequencies, degrading signal quality
- **Mitigation:** The system can increase transmit power, switch to more robust modulation schemes, or rely on satellite diversity (multiple satellites in view)
- **Impact on Availability:** In heavy-rain regions, availability may drop to 97–98% compared to 99.9%+ in clear-sky conditions

**Evidence:** Lab 05 analyzed weather impact on availability. Lab 06 simulated environmental degradation in the Packet Tracer model.

**Security+ Connection (1.2-C Availability, 3.4-C Resilience Testing):** Weather-induced degradation is an availability concern that terrestrial networks (cellular and fiber) do not face at the same severity.

---

## SECTION 3 — SPACE SEGMENT — CONSTELLATION ROUTING

### Satellite Reception and Onboard Processing

The LEO satellite receives the terminal's encrypted uplink signal and processes it:

- **Onboard Processing:** Unlike older "bent-pipe" satellites that simply amplify and retransmit, Starlink satellites perform onboard routing — decoding, switching, and re-encoding data
- **Demodulation and Remodulation:** The satellite demodulates the received signal, reads the addressing information, and remodulates it for the next leg of the journey

### Inter-Satellite Laser Links (ISLs)

Starlink satellites are equipped with optical inter-satellite links — laser terminals operating at approximately 1064 nm (infrared):

- **Capacity:** Up to 200 Gbps per link (gen 2+ satellites)
- **Distance:** Up to 5,300+ km between satellites
- **Mesh Network:** The constellation forms a mesh in space — traffic can route through multiple satellites before reaching a gateway
- **Latency Benefit:** By routing through space, traffic can bypass ground infrastructure entirely for long-distance paths. A packet from New York to London can travel via laser between satellites in ~50 ms, faster than the fastest submarine fiber cable

**Evidence:** Lab 01 documented the constellation architecture with ISL specifications cited from eoportal.org and starlink.com/technology.

### Orbital Mechanics and Handover

LEO satellites orbit at approximately 550 km altitude, completing an orbit in about 95 minutes. From any given ground location, a satellite is visible for only a few minutes:

- **Visibility Window:** Typically 4–10 minutes per satellite (depending on elevation angle and constellation density)
- **Handover Frequency:** The terminal must switch to a new satellite every few minutes — far more frequently than a cellular phone changes towers
- **Handover Process:** The terminal acquires the next satellite, transfers the session, and releases the old link. This is designed to be seamless, but brief packet loss or latency spikes can occur

**Evidence:** Lab 05 calculated visibility windows from orbital velocity. Lab 06 simulated handover gaps in Packet Tracer.

**Security+ Connection (3.4-A High Availability):** Constant handover is a fundamental availability challenge unique to LEO satellite networking. The system must maintain session continuity despite the infrastructure literally flying away at 7.6 km/s.

---

## SECTION 4 — DOWNLINK TO GATEWAY

### Gateway Ground Stations

The satellite downlinks traffic to a gateway ground station:

- **Gateway Architecture:** Each gateway site houses multiple radome-enclosed antennas (typically 9+ per site), connected via high-capacity fiber to Internet exchange points
- **Frequency:** Gateways use Ka-band (~17.7–21.2 GHz downlink, ~27.5–31 GHz uplink) and E-band (~71–86 GHz) for higher-capacity feeder links — different frequencies from the user terminal links
- **Global Distribution:** Approximately 150–170 gateway sites worldwide (as of early 2026), positioned near major IXPs and data-center PoPs for low-latency Internet handoff

**Evidence:** Lab 01 documented gateway architecture from SpaceX progress reports and FCC filings. Lab 04 assessed physical security of gateway sites using public satellite imagery.

### Decryption and Internet Handoff

At the gateway, the RF link encryption is terminated:

1. **Satellite Downlink:** Encrypted traffic arrives at the gateway antenna
2. **Decryption:** Gateway decrypts the link-layer encryption (AES-256), revealing plaintext IP packets
3. **Internet Routing:** Plaintext traffic enters the Internet backbone via the gateway's fiber connection to an IXP or peering point
4. **TLS Still Required:** From this point forward, security depends on the application layer — HTTPS/TLS must be used for end-to-end confidentiality

**Evidence:** Lab 03 documented the encryption termination point. Lab 04 analyzed the trust boundary this creates.

**Security+ Connection (1.2-A Confidentiality, 3.2-C Secure Communication):** The gateway is a critical trust boundary. Link-layer encryption ends here; application-layer encryption (TLS) continues. If TLS is not used, the traffic is plaintext on the Internet — identical to Mission 01's cellular architecture.

---

## SECTION 5 — INTERNET TRANSIT

### Peering Points and Route Propagation

From the gateway, traffic enters the public Internet:

- **Internet Exchange Points (IXPs):** Gateways peer directly with major networks at IXPs, minimizing latency and hops
- **BGP Routing:** Border Gateway Protocol decides path selection across autonomous systems
- **CDN and Edge Caching:** Google's CDN may serve content from edge nodes co-located at the same IXPs where Starlink gateways peer

**Evidence:** Lab 02 compared satellite and terrestrial Internet transit — both converge at the IXP/BGP level.

**Security+ Connection (3.1-A On-Premises Architecture):** Once traffic leaves the gateway, it faces the same BGP hijacking, route leak, and DDoS risks as any Internet traffic. Mission 01 documented these in Lab 06 (Routing Failure).

### Latency Considerations

A typical Starlink Terminal → Google journey involves:

|Hop|Approximate Latency|
|---|---|
|Terminal → Satellite (uplink)|2–4 ms (speed of light, ~550 km)|
|Satellite → Satellite (ISL, if used)|5–20 ms (variable)|
|Satellite → Gateway (downlink)|2–4 ms (~550 km)|
|Gateway → Internet → Google Edge|10–50 ms (terrestrial fiber)|
|Google Processing|10–50 ms|
|**Total Round Trip**|**25–100 ms (typical), median ~25–35 ms (US)**|

Compare to Mission 01 cellular:

|Hop|Approximate Latency|
|---|---|
|Phone → gNodeB|1–5 ms|
|gNodeB → Carrier Core|5–20 ms|
|Carrier → Internet|10–50 ms|
|Internet → Google Edge|20–100 ms|
|Google Processing|10–50 ms|
|**Total Round Trip**|**50–250 ms**|

Despite the 550-kilometer trip to space, Starlink's median latency (~25–35 ms in the US) is competitive with terrestrial broadband and vastly superior to legacy GEO satellite (~599+ ms). This is a direct consequence of LEO altitude choice.

**Evidence:** Lab 05 calculated theoretical latencies from the speed of light. Lab 07 researched observed performance data from Ookla and Starlink's network updates.

---

## SECTION 6 — GOOGLE INFRASTRUCTURE

### Edge Servers and Load Balancers

Once traffic reaches Google's infrastructure, the journey is identical to Mission 01:

- **Frontend Load Balancers:** Distribute requests across backend pools
- **TLS Termination:** HTTPS decryption occurs at the edge
- **WAF (Web Application Firewall):** Filters malicious requests

Google's infrastructure does not know or care whether the traffic arrived via cellular, satellite, or fiber — it's all IP packets.

**Evidence:** Lab 02 compared the application-layer experience on both architectures and found them identical. Mission 01 Labs 04–05 documented TLS termination and certificate validation.

### Application Processing

Google's application stack processes the request identically regardless of transport:

- HTTP handling, search index lookup, response generation
- Security headers (HSTS, CSP, X-Frame-Options) applied to responses
- Content compression (GZIP/Brotli)

**Evidence:** Mission 01 Lab 09 ran vulnerability scans on web applications (DVWA). The web application security principles are transport-agnostic.

---

## SECTION 7 — THE RETURN PATH

### Reverse Journey

Google's response travels back to the user via roughly the reverse path:

1. Google → Internet → Starlink Gateway (terrestrial fiber)
2. Gateway encrypts and uplinks to satellite (Ka-band/E-band)
3. Satellite routes via ISL (if needed) and downlinks to terminal (Ku-band)
4. Terminal decrypts and forwards to user device (Wi-Fi/Ethernet)

### Asymmetric Routing

As with Mission 01, the return path may not be symmetric:

- Outbound traffic may use Satellite A → Gateway X
- Return traffic may arrive via Satellite B → Gateway Y
- The terminal accepts traffic from whichever satellite is currently in view

**Security+ Connection (4.1-G Monitoring Computing Resources):** The terminal maintains connection state across handovers. TCP sequence numbers and acknowledgment logic must survive the satellite switch — a challenge that cellular systems face only when the user is moving, but satellite systems face constantly due to moving infrastructure.

**Evidence:** Lab 06 simulated asymmetric routing and handover in Packet Tracer. Lab 07 documented how the terminal maintains session state.

---

## SECTION 8 — SECURITY THROUGHOUT

### Confidentiality

|Layer|Protection Mechanism|Evidence Source|
|---|---|---|
|Application|HTTPS/TLS encryption|Mission 01 Labs 04–05; Mission 02 Lab 03 (comparison)|
|Link (RF)|AES-256 link encryption (hardware-fused keys)|Mission 02 Lab 03|
|ISL (satellite-to-satellite)|Presumed encrypted (proprietary)|Mission 02 Lab 01, 03 (research)|

**Gap:** Link-layer encryption terminates at the gateway. Without TLS, traffic is plaintext on the Internet backbone. **Recommendation:** Always use HTTPS. DNS should use DoH (DNS-over-HTTPS) to prevent resolver eavesdropping.

### Integrity

|Layer|Protection Mechanism|Evidence Source|
|---|---|---|
|Application|TLS MAC/AEAD|Mission 01 Lab 05|
|Link (RF)|Encryption includes integrity protection (AES-GCM or similar)|Mission 02 Lab 03 (inferred from AES-256 + mutual auth)|
|Transport|TCP checksum|Mission 01 Lab 04|

### Authentication

|Point|Method|Evidence Source|
|---|---|---|
|Terminal to Network|Certificate-based (STSAFE-A110, EAL5+)|Mission 02 Labs 01, 03, 04|
|Browser to Google|TLS certificate chain validation|Mission 01 Lab 05; identical for satellite|
|GPS to Terminal|GNSS signal (unencrypted by default)|Mission 02 Lab 01 (research)|

### Authorization

Authorization decisions occur at multiple points:

- **Network Access:** Terminal must be registered to an active account (SpaceX controls authorization)
- **Gateway Routing:** Only authenticated terminals can send traffic through the gateway
- **Google Access Control:** Account-based authorization for Google services (identical to Mission 01)

### Attack Surface Map

Every component is a potential compromise point:

|Component|Attack Vector|Mitigation|Evidence Source|
|---|---|---|---|
|User Terminal|Theft, tampering, firmware bypass (mod chip)|Secure mounting, tamper-resistant hardware, remote deactivation|Labs 03, 04, 08|
|Wi-Fi Network|Weak WPA2, rogue APs|WPA3, strong passphrase|Lab 08|
|RF Link (Ku-band)|Eavesdropping, jamming, spoofing|AES-256 encryption, spread spectrum, mutual auth|Labs 03, 08|
|Satellite|Command intrusion, ASAT|Encrypted command links, orbital maneuverability|Labs 03, 08|
|Inter-Satellite Link|Interception (very difficult)|Optical laser, narrow beam, encrypted|Lab 01, 03|
|Gateway Station|Physical breach, insider threat, network intrusion|Fencing, CCTV, access controls, redundant sites|Labs 04, 08|
|Fiber Backhaul|Cable cut, interception|Redundant paths, buried cable|Labs 04, 08|
|Internet Transit|BGP hijacking, DDoS|RPKI, DDoS mitigation|Mission 01 Lab 06; Lab 02|
|Google Edge|DDoS, application exploits|WAF, DDoS mitigation, bug bounty|Mission 01 Lab 09|

**Evidence:** Lab 08 produced a comprehensive threat model with 12+ catalogued threats across all components.

### Where Security Fails

Realistic failure modes include:

1. **Terminal Firmware Compromise:** Fault-injection attack bypasses authentication (Wouters, 2022)
    - Mitigation: Tamper-resistant hardware, firmware signing, secure boot
2. **RF Jamming:** Attacker transmits noise on Ku-band frequencies near the terminal
    - Mitigation: Spread-spectrum techniques, power adaptation, frequency agility
3. **Gateway Insider Threat:** Employee with network access intercepts plaintext traffic
    - Mitigation: Access controls, logging, job rotation, TLS (end-to-end encryption limits damage)
4. **Supply Chain Implant:** Hardware modified during manufacturing
    - Mitigation: Hardware key provisioning (STSAFE), vendor management, secure supply chain
5. **BGP Hijacking:** Traffic redirected through hostile networks (same as cellular)
    - Mitigation: RPKI, route filtering
6. **Power Loss:** Terminal has no battery — immediate service loss
    - Mitigation: Customer-provided UPS or generator

**Evidence:** Labs 03, 04, and 08 documented each failure mode with likelihood, impact, and mitigations.

---

## COMPARATIVE ANALYSIS — SATELLITE VS. CELLULAR

### Architectural Convergence and Divergence

|Dimension|Cellular (Mission 01)|Satellite (Mission 02)|Analysis|
|---|---|---|---|
|**Last-mile medium**|5G NR radio (sub-6 GHz / mmWave)|Ku-band RF (~12-14 GHz)|Different frequencies, same principle (wireless RF)|
|**Distance to first hop**|~1-5 km (cell tower)|~550 km (LEO satellite)|Satellite has higher floor latency|
|**Infrastructure mobility**|Fixed (towers don't move)|Moving (satellites orbit at 7.6 km/s)|Fundamental architectural difference|
|**Handover trigger**|User movement between cells|Satellite movement over user|Reversed: in satellite, the infrastructure moves; in cellular, the user moves|
|**Link encryption**|5G encryption (SIM-based)|AES-256 (hardware-fused keys)|Similar strength, different key management|
|**Authentication**|SIM credential (5G AKA)|Hardware certificate (STSAFE-A110)|Both use device-bound identity, different mechanisms|
|**Encryption termination**|Carrier core (PGW/UPF)|Gateway station|Both terminate at operator infrastructure → TLS still needed|
|**Physical security of infrastructure**|Towers fenced, but accessible|Gateways fenced; satellites physically inaccessible|Satellite infrastructure is harder to physically attack|
|**Weather impact**|Minimal|Moderate (rain fade at Ku/Ka-band)|Satellite has environmental vulnerability|
|**Power resilience**|Phone has battery|Terminal has NO battery|Cellular has edge for power resilience|
|**Geographic coverage**|Limited to tower coverage area|Near-global (wherever sky is visible)|Satellite wins for remote/maritime|
|**Handover frequency**|Low (only when moving)|High (every 4-10 minutes)|Satellite has more handover challenges|
|**Redundancy model**|Multiple towers in range|Multiple satellites in view, multiple gateways|Both rely on infrastructure diversity|
|**Application layer**|HTTP/HTTPS, TCP, DNS, TLS|HTTP/HTTPS, TCP, DNS, TLS|**Identical** — convergence point|
|**Internet transit**|BGP, IXPs, CDNs|BGP, IXPs, CDNs|**Identical** — convergence point|

### When to Use Each Architecture

**Satellite excels when:**

- No terrestrial infrastructure exists (remote, rural, maritime, aviation)
- Disaster recovery (cell towers destroyed, fiber cut)
- Mobility beyond cellular coverage (ships, aircraft, expeditions)
- Rapid deployment (no tower construction needed)

**Cellular excels when:**

- Population density justifies tower deployment (urban, suburban)
- Latency-sensitive applications require consistent <20 ms (gaming, real-time control)
- Weather resilience is critical (tropical, high-rainfall regions)
- Power independence is needed (phone battery survives outages)
- Physical infrastructure security is manageable (towers are accessible and defensible)

**Hybrid scenarios:**

- Starlink backhaul for a remote cellular tower (brings cellular service to a remote area using satellite for the backhaul connection)
- Cellular for primary, satellite for backup (resilience through platform diversity)

### Security Properties: Equivalent vs. Divergent

**Equivalent security properties:**

- End-to-end confidentiality depends entirely on TLS/HTTPS in both architectures
- Internet transit threats (BGP hijacking, DDoS, DNS manipulation) are identical
- Application-layer security (web vulnerabilities, SQL injection, XSS) is transport-agnostic
- Insider threat at the operator (carrier or SpaceX) is structurally similar

**Divergent security properties:**

- Satellite has unique RF attack vectors (jamming, spoofing at Ku-band) that cellular faces less severely
- Satellite has unique physical security advantage (satellites are physically inaccessible)
- Satellite has unique availability vulnerability (rain fade, no terminal battery, constant handover)
- Cellular has unique physical security vulnerability (towers are climbable and accessible)
- Cellular has unique attack vector (IMSI catchers, rogue base stations)

---

## CONCLUSION

### What Makes This System Secure?

The Terminal → Google satellite journey achieves security through the same **defense in depth** principle as Mission 01, adapted for space:

1. **Multiple Layers of Encryption:** AES-256 at the RF link layer, TLS at the application layer — each protecting a different trust boundary
2. **Hardware-Bound Authentication:** Terminal identity is cryptographically tied to physical hardware (STSAFE-A110), making cloning difficult
3. **Physical Inaccessibility of Core Infrastructure:** Satellites cannot be physically tampered with by non-nation-state actors
4. **Redundancy at Every Layer:** Multiple satellites, multiple gateways, multiple fiber paths — the system degrades gracefully rather than failing completely
5. **Regulatory Oversight:** FCC licensing, ITU coordination, and debris mitigation rules create accountability

### Where Are Its Weaknesses?

1. **No End-to-End Encryption by Default:** Link-layer encryption terminates at the gateway. Without HTTPS, traffic is plaintext on the Internet backbone
2. **RF Vulnerability:** Ku-band signals can be jammed or intercepted (though encrypted)
3. **Terminal Power Dependency:** No battery means any power interruption kills service immediately
4. **Weather Sensitivity:** Rain fade degrades availability in tropical or high-rainfall regions
5. **Constant Handover:** Frequent satellite transitions create opportunities for brief service interruptions
6. **Operator Trust:** Users must trust SpaceX not to inspect traffic at the gateway — same trust model as trusting a cellular carrier
7. **Supply Chain Risk:** Terminal hardware comes from a single manufacturer — if the supply chain is compromised, all terminals are at risk

### What Could Break?

1. **Terminal Firmware Bypass:** A hardware fault-injection attack (demonstrated by Wouters) could allow unauthorized terminal access
2. **Coordinated RF Jamming:** An attacker near a terminal could deny service by jamming Ku-band frequencies
3. **Gateway Compromise:** Physical or network intrusion at a gateway could expose aggregated subscriber traffic
4. **Constellation Depletion:** Anti-satellite weapons or debris cascade could reduce constellation capacity
5. **Regulatory Shutdown:** A government could revoke spectrum licenses, halting service in a region
6. **Backhaul Fiber Cut:** Cutting the fiber between a gateway and its IXP isolates that gateway's traffic

### What Would Evidence of Compromise Look Like?

Drawing from Labs 06, 07, and 08:

- **Sudden Latency Spikes Without Weather Correlation:** Could indicate RF interference or jamming
- **Unexpected Satellite Handover Patterns:** Could indicate signal spoofing or rogue satellite
- **Abnormal Traffic Volume at Gateway:** Could indicate data exfiltration or compromise
- **Terminal Firmware Version Anomalies:** Could indicate unauthorized firmware modification
- **Unauthorized Devices on Local Network:** Could indicate Wi-Fi compromise or physical access
- **Repeated Authentication Failures:** Could indicate attempts to clone a terminal identity
- **Signal Strength Anomalies:** Sudden drops without environmental cause could indicate deliberate interference

**Security+ Mapping:** This conclusion ties to Domain 2 (threat analysis — RF attacks, physical attacks), Domain 3 (architecture — resilience, redundancy), Domain 4 (operations — monitoring, diagnostics), and Domain 5 (risk analysis — threat modeling, regulatory compliance).

---

## APPENDICES

### Appendix A — Evidence Inventory

|Artifact|Lab|Description|
|---|---|---|
|`mission02-lab01-architecture-diagrams.drawio`|01|Level 0–2 satellite architecture diagrams|
|`mission02-lab01-protocol-stack.md`|01|Protocol stack mapping at each link boundary|
|`mission02-lab02-comparison-table.md`|02|Master terrestrial vs. satellite comparison table|
|`mission02-lab02-latency-calculations.md`|02|Theoretical latency calculations (LEO vs. GEO vs. cellular)|
|`mission02-lab03-rf-security-analysis.md`|03|RF frequency, encryption, and attack vector analysis|
|`mission02-lab04-physical-security-assessment.md`|04|Gateway site analysis and physical attack surface map|
|`mission02-lab05-availability-analysis.md`|05|Redundancy, power, and availability model|
|`mission02-lab06-failure-simulations.pkt`|06|Packet Tracer satellite model with failure scenarios|
|`mission02-lab06-failure-taxonomy.md`|06|Extended failure taxonomy (satellite-specific)|
|`mission02-lab07-diagnostic-data-analysis.md`|07|Public performance data and diagnostic data model|
|`mission02-lab08-threat-model.md`|08|Complete threat model with risk register|
|`mission02-lab08-risk-register.csv`|08|12+ catalogued threats with likelihood and impact|
|`mission02-lab09-regulatory-analysis.md`|09|FCC/ITU regulatory framework documentation|
|`mission02-lab10-final-narrative.md`|10|This document|

### Appendix B — Security+ Atomic Coverage Summary

|Domain|Requirements Addressed|Key Examples|
|---|---|---|
|1. General Concepts|1.1-A,B,D,E,F,G,H,I, 1.2-A,B,C,E,F, 1.3-B, 1.4-B,E|Controls, CIA triad, encryption, authentication|
|2. Threats & Vulnerabilities|2.1-A,D,H, 2.2-B,F,G,H, 2.3-B,H, 2.4-D,E, 2.5-B,C,D,E,F|Threat actors, attack vectors, physical attacks, hardware vulns|
|3. Architecture|3.1-A,B, 3.2-A,B,C,D, 3.3-B,C, 3.4-A,B,C,D,E,G|Infrastructure, secure comms, resilience, HA|
|4. Operations|4.1-D,G, 4.2-D, 4.3-A,B,C,D, 4.4-A,B, 4.8-C,D, 4.9-A,B|Wireless security, monitoring, vulnerability lifecycle, IR|
|5. Program Management|5.1-E, 5.2-A,B,C,G, 5.4-D|External considerations, risk analysis, privacy|

**Total:** ~55 atomic requirements addressed across Mission 02

### Appendix C — Comparative Evidence (Links to Mission 01)

|Mission 01 Artifact|Mission 02 Comparison Point|
|---|---|
|`mission01-lab01-simple-journey.pkt`|Mission 02 Lab 02: Side-by-side architecture comparison|
|`mission01-lab04-http-capture.pcapng`|Mission 02 Lab 03: TLS vs. RF link encryption comparison|
|`mission01-lab05-tls-analysis.md`|Mission 02 Lab 03: Encryption termination points compared|
|`mission01-lab06-routing-failure.pkt`|Mission 02 Lab 06: Failure taxonomy extension|
|`mission01-lab07-firewall-config.txt`|Mission 02 Lab 02: Security control comparison|
|`mission01-lab09-vuln-report.md`|Mission 02 Lab 08: Threat model comparison|
|`mission01-lab11-incident-report.md`|Mission 02 Lab 08: IR methodology applied to satellite threats|
|`mission01-final-narrative.md`|This document: Side-by-side narrative comparison|

### Appendix D — References

- starlink.com/technology — Official Starlink technical overview
- starlink.com/updates — Network performance updates (2025–2026)
- starlink.com/public-files/starlinkProgressReport_2025.pdf — SpaceX progress report
- eoportal.org/satellite-missions/starlink — Spacecraft specifications
- en.wikipedia.org/wiki/Starlink — Curated, cited summary
- starlink.sx — Public constellation tracker
- FCC 47 CFR Part 25 — Satellite communications regulations
- FCC 5-Year Deorbit Rule (September 2022)
- ITU Radio Regulations (Articles 9 and 11)
- Wouters, L. (2022). "Glitched on Earth by Humans" — Black Hat USA
- DarkNavy. "A First Glimpse of the Starlink User Terminal" — Terminal firmware analysis
- Ookla Speedtest. "2025 Global Satellite Broadband Performance Report"
- CompTIA Security+ SY0-701 Exam Objectives
- RFC 2818 (HTTP Over TLS)
- RFC 5280 (Internet X.509 PKI)
- 3GPP TS 33.501 (5G Security Architecture) — for comparison

---

## END OF MISSION 02 FINAL EXPLANATION

_Document Version: 1.0_ _Date: August 15, 2026_ _Author: Mission 02 Learner_ _Review Status: Pending Security+ Coverage Validation_