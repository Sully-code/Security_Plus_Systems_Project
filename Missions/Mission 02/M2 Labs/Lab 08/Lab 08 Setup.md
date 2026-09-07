## LAB 08 — Threat Modeling

### Objective

Create a comprehensive threat model for the Starlink satellite network. Identify threat actors, attack vectors, potential impacts, and mitigations. This lab formalizes the security analysis from Labs 03–07 into a structured threat model document.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|2.1-A|Nation-state actors|🟡 Understood|Nation-state threat analysis (jamming, ASAT, cyber)|
|2.1-D|Insider threats|🟡 Understood|Insider threat scenarios for ground stations|
|2.1-H|Espionage|🟡 Understood|Signal interception and traffic analysis threats|
|2.2-H|Attack surfaces|🟢 Demonstrated|Complete attack surface map for satellite system|
|5.2-A|Risk identification|🟢 Demonstrated|Risks identified across all system components|
|5.2-B|Risk assessment|🟢 Demonstrated|Risk assessment with likelihood and impact|
|5.2-C|Risk analysis|🟢 Demonstrated|Quantitative and qualitative risk analysis|
|2.2-G|Vulnerable software|🟡 Understood|Terminal firmware vulnerability analysis|
|2.3-B|Hardware vulnerabilities|🟢 Demonstrated|Terminal hardware vulnerability (mod chip attack)|
|2.3-H|Supply chain vulns|🟡 Understood|Hardware/firmware supply chain risks|

### Prerequisites

Labs 01–07 complete.

### Tools

- draw.io
- Web browser (research)
- Markdown/text editor

### Procedure

**Step 1 — Identify threat actors**

Research and document each actor type relevant to satellite systems:

|Actor|Capability|Motivation|Likelihood|Examples|
|---|---|---|---|---|
|Nation-state|Advanced cyber, ASAT, electronic warfare|Strategic disruption, espionage|Low-Medium|Documented GPS spoofing, ASAT tests|
|Organized crime|Cyber intrusion, social engineering|Financial gain, data theft|Low|Minimal direct satellite targeting|
|Insider (ground station personnel)|Physical access, network access|Sabotage, data theft, coercion|Low|All systems face insider risk|
|Hacker/researcher|Technical skills, limited resources|Discovery, fame, disclosure|Medium|Wouters' $25 mod chip attack|
|Unintentional actor|RF interference, misconfiguration|None (accidental)|Medium|Adjacent frequency interference|
|Activist/hacktivist|Variable cyber capability|Political statement|Low|Unlikely to target space infrastructure|

Sources: IEEE security papers, NSA/Australian Cyber Security Centre advisories, academic threat models

**Step 2 — Map the complete attack surface**

Consolidate all attack surfaces identified in previous labs:

`┌─────────────────────────────────────────────────────────┐ │ ATTACK SURFACE MAP │ ├─────────────────────────────────────────────────────────┤ │ │ │ USER SITE │ │ ├── Terminal physical access (theft, tampering) │ │ ├── Wi-Fi network (if WPA2/WPA3 not secured) │ │ ├── Local network access (rogue devices) │ │ ├── Terminal firmware (exploitation, mod chip) │ │ ├── Power supply (disruption) │ │ └── Terminal supply chain (counterfeit components) │ │ │ │ RF LINK │ │ ├── Ku-band downlink eavesdropping │ │ ├── Ku-band uplink jamming │ │ ├── Signal spoofing (false satellite/terminal) │ │ ├── RF replay attacks │ │ └── RF interference (accidental or deliberate) │ │ │ │ SPACE SEGMENT │ │ ├── Satellite command intrusion │ │ ├── Telemetry spoofing │ │ ├── ISL interception (theoretically very difficult) │ │ ├── ASAT (kinetic, laser dazzling) │ │ └── Orbital debris (accidental) │ │ │ │ GROUND INFRASTRUCTURE │ │ ├── Gateway physical breach │ │ ├── Gateway network intrusion │ │ ├── Insider threat (personnel) │ │ ├── Fiber backhaul cut/interception │ │ ├── Power disruption at gateway │ │ └── DNS/routing manipulation at peering point │ │ │ └─────────────────────────────────────────────────────────┘`

**Step 3 — Build the risk register**

For each identified threat, assess:

|ID|Threat|Actor|Vector|Likelihood (1-5)|Impact (1-5)|Risk Score (L×I)|Current Mitigations|Residual Risk|
|---|---|---|---|---|---|---|---|---|
|T01|RF jamming of user terminal|Nation-state|RF (Ku-band)|2|4|8|Spread spectrum, power adaptation|Medium|
|T02|Terminal firmware bypass (mod chip)|Hacker/researcher|Hardware fault injection|3|3|9|STSAFE-A110, secure boot|Medium|
|T03|Gateway physical breach|Insider/activist|Physical access|1|5|5|Fencing, locks, CCTV|Low|
|T04|Satellite command intrusion|Nation-state|Cyber (command uplink)|1|5|5|Encrypted command links, authentication|Low|
|T05|RF eavesdropping (downlink)|Nation-state|RF reception|3|2|6|AES-256 link encryption|Low|
|T05|Signal spoofing|Nation-state|RF transmission|2|3|6|Mutual authentication, crypto signatures|Low-Medium|
|T06|Fiber backhaul cut|Various|Physical (cable cut)|2|4|8|Redundant paths, alternate gateways|Medium|
|T07|Insider data access at gateway|Insider|Network access|2|3|6|Access controls, logging|Medium|
|T08|Supply chain implant|Nation-state|Manufacturing|1|4|4|Hardware key provisioning, vendor management|Low|
|T09|Accidental RF interference|Unintentional|RF (adjacent band)|3|2|6|Frequency coordination, filtering|Low-Medium|
|T10|ASAT (kinetic)|Nation-state|Military|1|5|5|Orbital maneuverability, constellation size|Low|
|T11|Wi-Fi compromise (user site)|Various|Network (Wi-Fi)|3|3|9|WPA3, user configuration|Medium|
|T12|DNS manipulation at peering|Various|Network (BGP/DNS)|2|4|8|DNSSEC, redundant resolvers|Medium|

**Step 4 — Analyze the top risks**

Select the top 5 risks by score and perform deeper analysis:

For each:

1. **Attack chain:** How would this attack unfold step by step?
2. **Detection:** What diagnostic data would reveal it? (Connect to Lab 07)
3. **Containment:** What could be done immediately?
4. **Eradication:** What would permanently fix it?
5. **Recovery:** How would service be restored?
6. **Lessons learned:** What systemic change would prevent recurrence?

**Step 5 — Create the threat model diagram**

In draw.io, create a comprehensive threat model showing:

- All system components (from Lab 01)
- All attack vectors (from Step 2)
- Trust boundaries (where data crosses between trust zones)
- Control placement (where mitigations are deployed)

Use a color-coding scheme:

- Green: Protected by encryption
- Yellow: Protected by physical controls
- Orange: Protected by authentication
- Red: Unmitigated residual risk

**Step 6 — Compare with Mission 01 threat landscape**

|Threat Category|Mission 01 (Cellular)|Mission 02 (Satellite)|
|---|---|---|
|RF interception|5G encryption|Ku-band encryption (similar)|
|RF jamming|Possible (rare)|More feasible (weaker signals from space)|
|Physical access to infrastructure|Cell tower (accessible)|Gateway (remote, fenced); satellite (inaccessible)|
|Insider threat|Carrier employee|SpaceX employee (similar)|
|Supply chain|Phone manufacturer|Terminal manufacturer (similar)|
|Network attacks|BGP hijack, DNS poisoning|Same (Internet routing is shared)|
|Unique to satellite|—|ASAT, orbital debris, rain fade|
|Unique to cellular|—|IMSI catchers, rogue base stations|

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Threat actor analysis|Threat model document|
|Complete attack surface map|Attack-surface map|
|Risk register (12+ threats)|Part of threat model|
|Top-5 risk deep analysis|Part of threat model|
|Threat model diagram (draw.io)|Threat-vector map|
|Mission 01 vs 02 threat comparison|Part of technical report|

### Success Criteria

- At least 6 threat actors are documented with capabilities and motivations
- Attack surface map covers user site, RF link, space segment, and ground infrastructure
- Risk register has at least 12 entries with likelihood, impact, and risk scores
- Top 5 risks have complete attack chain and IR lifecycle analysis
- Threat model diagram is comprehensive and color-coded by control type
- Comparison with Mission 01 identifies shared and unique threats

### Curiosity Branches

- What is the STRIDE threat modeling framework? (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege)
- How does the NSA assess satellite communication security?
- What happened when Russia reportedly jammed Starlink signals in Ukraine?
- What is electronic warfare (EW) and how does it apply to civilian satellite systems?