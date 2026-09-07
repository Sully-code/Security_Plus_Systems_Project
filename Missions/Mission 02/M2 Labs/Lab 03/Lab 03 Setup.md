## LAB 03 — RF Security Investigation

### Objective

Research and analyze the security of the satellite RF link. Understand what frequency bands are used, how the link is encrypted, what authentication mechanisms protect terminal access, and what attacks are theoretically possible against the RF layer.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|1.4-B|Encryption|🟢 Demonstrated|RF link encryption analysis (AES-256, hardware keys)|
|4.1-D|Wireless security|🟢 Demonstrated|Satellite RF security investigation documented|
|2.4-E|Network attacks|🟢 Demonstrated|RF jamming, spoofing, eavesdropping analyzed|
|2.2-B|Unsecure network vectors|🟢 Demonstrated|RF interception risks documented|
|1.2-A|Confidentiality|🟢 Demonstrated|Link encryption confidentiality analysis|
|1.2-E|Authentication|🟢 Demonstrated|Terminal-to-network authentication mechanism documented|
|1.1-B|Preventive controls|🟢 Demonstrated|Encryption and authentication as preventive controls|
|1.1-F|Detective controls|🟢 Demonstrated|Anomaly detection and link monitoring|

### Prerequisites

Lab 01 complete. Mission 01 Lab 05 (TLS Investigation) complete for comparison.

### Tools

- Web browser (research)
- draw.io
- Wireshark (for comparing with Mission 01 TLS captures)
- Mission 01 Lab 04/05 artifacts (for comparison)

### Procedure

**Step 1 — Document the RF frequency landscape**

Research and document the frequency bands used at each link in the Starlink system:

|Link Segment|Direction|Frequency Band|Approximate Range|Purpose|
|---|---|---|---|---|
|User terminal → Satellite|Uplink|Ku-band (~14–14.5 GHz)|?|User data uplink|
|Satellite → User terminal|Downlink|Ku-band (~10.7–12.7 GHz)|?|User data downlink|
|Gateway → Satellite|Uplink|Ka-band (~27.5–31 GHz) or E-band (~81–86 GHz)|?|Feeder link uplink|
|Satellite → Gateway|Downlink|Ka-band (~17.7–21.2 GHz) or E-band (~71–76 GHz)|?|Feeder link downlink|
|Satellite → Satellite|Bidirectional|Optical (~1064 nm infrared laser)|?|Inter-satellite link|

Sources: FCC filings, starlink.com/technology, academic papers

For each band, document:

- Why this band was chosen (bandwidth vs. propagation tradeoffs)
- Rain fade characteristics (higher frequencies attenuate more in rain)
- Regulatory status (licensed, shared, coordinated)

**Step 2 — Analyze the link-layer encryption model**

Research the terminal's security architecture:

Based on public research (including the KU Leuven analysis by Lennert Wouters and the DarkNavy firmware analysis):

1. **Main SoC:** Custom SpaceX system-on-chip with hardware-fused encryption keys
2. **Security chip:** STSAFE-A110 (Common Criteria EAL5+ rated)
3. **Authentication mechanism:** Terminal presents a cryptographically signed certificate stored on the secure element
4. **Payload encryption:** AES-256 symmetric cipher with mutual authentication

Document the encryption chain:

`User data → Encrypted at terminal (AES-256, hardware key) → RF uplink (encrypted) → Satellite processing (may decrypt and re-encrypt for ISL) → RF downlink to gateway (encrypted) → Gateway decryption → Plain IP traffic enters Internet backbone`

**Compare with Mission 01 TLS model:**

|Property|TLS (Mission 01)|Starlink RF Link (Mission 02)|
|---|---|---|
|Encryption layer|Application/Transport (Layer 4-7)|Link layer (Layer 2)|
|Key exchange|Diffie-Hellman/ECDHE during TLS handshake|Hardware-fused keys, certificate-based|
|Key storage|Browser/OS certificate store|Dedicated security chip (STSAFE-A110)|
|Algorithm|Negotiated during handshake (e.g., AES-GCM, ChaCha20)|AES-256 (fixed)|
|Mutual authentication|Server authenticates to client (client auth optional)|Terminal and network mutually authenticate|
|Where encryption terminates|At the destination server (end-to-end HTTPS)|At the gateway (link-layer only; HTTPS still needed for end-to-end)|

Key insight: The RF link encryption protects against RF-layer eavesdropping, but it does NOT provide end-to-end confidentiality. Once traffic reaches the gateway and enters the Internet, it's plaintext IP — just like any other Internet traffic. HTTPS/TLS is still needed on top.

**Step 3 — Analyze RF attack vectors**

Research and document each attack type (theoretical only — no active testing):

**3a. RF Jamming:**

- What is it? Transmitting interference signals on the same frequency to drown out legitimate traffic
- How does it apply to Starlink? An attacker near a user terminal could transmit noise on Ku-band frequencies
- What is the impact? Denial of service — terminal cannot communicate with satellite
- What mitigations exist? Spread-spectrum techniques, frequency hopping, power adaptation
- Security+ classification: This is a network-layer DoS attack (2.4-E)

**3b. RF Eavesdropping:**

- What is it? Intercepting RF signals with appropriate receiving equipment
- How does it apply to Starlink? Ku-band downlink signals are broadcast over a wide area; anyone with a Ku-band receiver could theoretically capture them
- What is the impact? Without the encryption keys, captured data is unreadable (AES-256)
- What mitigations exist? Link-layer encryption makes captured traffic useless without keys
- Security+ classification: This is a confidentiality threat (1.2-A)

**3c. Signal Spoofing:**

- What is it? Transmitting fraudulent signals that appear to come from a legitimate source
- How does it apply to Starlink? Attacker could attempt to inject false data by mimicking satellite or terminal signals
- What is the impact? Potential for false data injection or MITM (if authentication is bypassed)
- What mitigations exist? Mutual authentication, certificate-based terminal identity, cryptographic signatures
- Security+ classification: Network attack, integrity threat (2.4-E, 1.2-B)

**3d. Terminal Firmware Attack:**

- What is it? Exploiting vulnerabilities in the terminal's firmware or hardware
- How does it apply to Starlink? Security researcher Lennert Wouters (KU Leuven) demonstrated a ~$25 mod chip that performs fault injection to bypass authentication
- What is the impact? Could allow unauthorized terminal access, key extraction, or network fraud
- What mitigations exist? Tamper-resistant hardware, secure boot chain, firmware signing
- Security+ classification: Hardware vulnerability (2.3-B), physical attack vector (2.4-D)

**Step 4 — Create the RF security model diagram**

In draw.io, create a diagram showing:

`┌──────────────┐ RF Link (Ku-band) ┌──────────────┐ │ USER │◄═════════════════════════════════►│ SATELLITE │ │ TERMINAL │ AES-256 encrypted │ │ │ │ Certificate-authenticated │ │ │ STSAFE-A110 │ Mutual authentication │ │ │ (EAL5+) │ │ │ └──────────────┘ └──────┬───────┘ │ Ka-band or optical ISL │ ┌──────▼───────┐ │ GATEWAY │ │ STATION │ │ │ │ Decryption │ │ occurs here │ └──────┬───────┘ │ Fiber (plaintext IP) │ ┌──────▼───────┐ │ INTERNET │ │ (TLS still │ │ needed for │ │ E2E security)│ └──────────────┘`

Annotate:

- Where encryption starts and stops
- Where authentication occurs
- Where an eavesdropper could intercept (but not read) traffic
- Where a jammer could disrupt service
- Where HTTPS/TLS is still needed on top of RF link encryption

**Step 5 — Compare with Mission 01 TLS captures**

Open your Mission 01 Lab 04 HTTPS capture in Wireshark. Contrast what an observer can see:

|Observation Point|Cellular (Mission 01)|Satellite (Mission 02)|
|---|---|---|
|On the RF link|5G encryption hides traffic|AES-256 link encryption hides traffic|
|At the carrier/gateway|Traffic is decrypted, routed as plaintext IP|Same — decrypted at gateway, routed as plaintext IP|
|On the Internet|Same for both — IP routing, TLS if HTTPS|Same for both|
|What can an RF eavesdropper see?|Metadata (signal strength, timing)|Metadata (signal strength, timing, frequency)|

Key finding: Both architectures rely on link-layer encryption for the wireless segment and TLS for end-to-end confidentiality. The layer is different, but the principle is the same.

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|RF frequency landscape table|RF link security analysis|
|Link encryption analysis document|RF link security analysis|
|RF attack vector analysis (4 types)|Part of technical report|
|RF security model diagram (draw.io)|Trust-boundary diagram (satellite variant)|
|TLS vs RF encryption comparison|Part of technical report|

### Success Criteria

- All frequency bands are documented with specific ranges and sources cited
- Learner can explain why link-layer encryption does NOT replace TLS/HTTPS
- Four RF attack vectors are analyzed with mitigations documented
- Security model diagram clearly shows where encryption starts/stops
- Comparison with Mission 01 TLS model is accurate and insightful

### Curiosity Branches

- What is spread-spectrum communication and how does it resist jamming?
- What is the STSAFE-A110 chip and what does EAL5+ certification mean?
- How did the KU Leuven researcher bypass Starlink's security? (Research the Black Hat presentation)
- Could quantum computing break the AES-256 link encryption?