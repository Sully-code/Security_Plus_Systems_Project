---

## PHONE → GOOGLE: A COMPLETE SYSTEMS JOURNEY

---

## INTRODUCTION

*[Own analysis — 2 paragraphs maximum]*

Paragraph 1: What happens when a phone requests `https://www.google.com`, stated in one
plain sentence, then the decomposition promise — dozens of components across radio,
carrier, Internet, and destination infrastructure, each applying controls.

Paragraph 2: The evidence discipline of this document: every claim is either cited to a
source (3GPP / Cisco / NIST / OWASP / MDN / Cloudflare / RFC Editor) or labeled as own
analysis; every laboratory claim points to a concrete artifact from Appendix A. Close with
one sentence pointing to the Mission 01 Passport for the full planned-coverage model
(four planning classes) and Artifact 22 for the complete Security+ matrix.

**Do not restate domains or counts here. Point to them.**

---

## SECTION 1 — BEFORE THE REQUEST: PHONE PREPARATION

### Cellular Identity and 5G-AKA Authentication

- **SIM/eSIM:** The USIM permanently stores the subscriber's long-term secret key **K**
  and identity **SUPI** (Subscription Permanent Identifier). K is never transmitted —
  it exists only on the USIM and in the carrier's UDM/ARPF.
  *[CITE: ShareTechnote 5G Security / CableLabs 4G-5G authentication paper]*

- **Registration:** On power-up or mobile-data enable, the UE sends a Registration
  Request over **5G NR** through the **gNodeB** to the **AMF** in the 5G Core. The
  request carries **SUCI** (the concealed SUPI) or a previously allocated **5G-GUTI**.
  *[CITE: 3GPP / CableLabs]*

- **Mutual authentication (5G-AKA):** AMF → (SEAF) → **AUSF** → **UDM/ARPF**, where
  **SIDF** de-conceals SUCI. The UDM issues the authentication vector
  (**RAND**, **AUTN**, **XRES***, K_AUSF). The USIM validates **AUTN** — proving the
  network is legitimate before responding (defense against rogue base stations /
  IMSI catchers) — then computes **RES*** using K. Both the visited AMF/SEAF (against
  **HXRES***) and the home **AUSF** (against XRES*) independently verify the response.
  *[CITE: free5GC / Mpirical / Award Solutions — pulled from Segment 1.2 corrections]*

- **Key derivation hierarchy:** Successful authentication seeds
  **K_AUSF → K_SEAF → K_AMF → K_gNB** — separate derived keys protect NAS signaling and
  the radio link. *[CITE: 3GPP AKMA]*

> ⚠️ TERMINOLOGY LOCK: Use AUSF/UDM/ARPF/SIDF exclusively. HSS/AuC, IMSI, and
> PDP Context are 4G terms and must not appear anywhere in this document.

**Evidence slot:** *[PLACEHOLDER — Artifact 3 (Level 2 diagram) + Artifact 4 (auth-flow
maps); insert one-sentence pointer to the actual executed lab evidence]*

**Security+ anchor:** 1.2-E (Demonstrated), 1.2-D (Understood — home-network independent
confirmation), 2.5-B (least-privilege key distribution — Understood).

### Data Session Establishment

- **PDU session** (NOT "PDP context"): after registration, the **SMF** establishes the
  PDU session and enforces policy on the **UPF**; the **PCF** supplies authorization
  policy (plan, roaming, services). *[CITE: Cisco 5G AMF guide — N11/N15 references]*

- **Addressing:** *[PLACEHOLDER — Segment 1.3 output: summarize which address the phone
  actually uses, how it is assigned, and CG-NAT treatment; completed in Segment 1.3]*

**Security+ connection:** 1.2-F Authorization (Demonstrated), 2.5-B Access control.

---

## SECTION 2 — APPLICATION LAYER: THE BROWSER

### URL Parsing
*[Own analysis]* Browser splits scheme / host / path; `https://` mandates TLS —
certificate failure = no connection. Keep to 2 sentences.

### DNS Resolution
- Browser checks local cache first; miss → recursive query to the configured resolver.
- Transport: plaintext UDP/53 vs. encrypted DNS (DoH/DoT) distinction.
  *[CITE: Cloudflare DNS page]*

**Security concerns to state explicitly:**
1. Plaintext DNS exposes queried domains to the carrier and on-path observers.
2. DNS manipulation → silent redirection to attacker infrastructure (phishing vector).
3. DNSSEC / encrypted DNS as mitigations. *[CITE: MDN or OWASP]*

**Evidence slot:** *[PLACEHOLDER — Lab 03 DNS capture findings; cite Artifact 10]*

### TLS 1.3 Session Establishment
*[TERMINOLOGY LOCK: TLS 1.3 per RFC 8446. Single round trip. ECDHE key exchange only —
no RSA key exchange, no static DH. Certificate chain arrives encrypted after the
ServerHello. AEAD cipher suites provide confidentiality + integrity in one mechanism.]*

Flow to document: ClientHello (key share + SNI) → ServerHello → {Certificate,
CertificateVerify, Finished} → client Finished → application data.
*[CITE: RFC 8446 §2 / §4]*

**Critical finding (keep — this is a Strength):** even under HTTPS, metadata remains
observable: source/destination IPs, packet sizes, timing, TLS SNI, TLS version.
Motivates DoH and ECH. *(own analysis, corroborated by [CITE: Cloudflare/Imperva])*

**Evidence slots:** *[PLACEHOLDER — Lab 05 certificate-chain inspection (OpenSSL) +
Lab 04 handshake capture; cite Artifacts 11–12. Resolve once, definitively, whether the
inspected endpoint is example.com or google.com — no internal contradictions.]*

**Security+ connections:** 1.4-A/B/D/E, 1.2-A/B, 3.2-C.

---

## SECTION 3 — RADIO ACCESS (HIGHWAY SCENARIO)

- **5G NR transmission:** modem → RF, licensed spectrum, QAM modulation. Keep to 3 bullets.
- **gNodeB = relay, not decider:** transparently relays NAS to the AMF; schedules radio
  resources; performs handover. *[CITE: Cisco 5G AMF — N2 reference point]*
- **Handover:** carriers perform intra-PLMN handover without dropping the session, reusing
  derived keys (K_gNB protects the radio link); rogue-gNodeB defense is the same mutual
  authentication validated in Segment 1.2 Q2. Label deep handover mechanics as a
  **curiosity branch** — do not claim it was simulated.
  *(own analysis; hardware constraint noted per free-tools guideline)*

**Evidence slot:** *[PLACEHOLDER — Artifact 3 documentation of handover position]*

**Security+ connection:** 4.1-D, 1.1-G (physical), 2.2-B.

---

## SECTION 4 — CARRIER CORE

- **Transport → regional routers → 5G Core (SMF/UPF):** aggregation, then session
  management and user-plane forwarding. *[CITE: Cisco 5G xHaul / AMF guides]*
- **CG-NAT:** many subscribers share public IPs at the carrier edge; translation point,
  resilience trade-off. *[PLACEHOLDER — Lab 02 evidence; cite Artifact 9]*
- **Controls:** ACLs / stateful filtering / rate limiting at carrier boundaries.
  **Evidence slot:** *[PLACEHOLDER — Lab 07 firewall ruleset and test results; cite
  Artifact 14]* **Security+:** 4.5-A (Demonstrated), 1.1-B preventive, 4.9-A logs.
- **Subscriber separation:** tunnel/segmentation isolation between users (GTP-style
  logical separation, presented conceptually). *(own analysis)*

---

## SECTION 5 — INTERNET TRANSIT

- **IXPs, transit providers, BGP path selection.** Keep to one paragraph.
- **BGP risk:** hijack / route-leak can steer traffic through hostile networks; mitigations
  = RPKI, route filtering. **Security+ lock: 2.4-E Network attacks (Demonstrated).**
  ❌ REMOVE: any tie of BGP to 3.1-F (IaC) or 3.1-A — false coverage; both are
  Understood/Encountered per Passport and neither demonstrates via BGP.
  **Evidence slot:** *[PLACEHOLDER — Lab 06 routing-failure simulation; cite Artifact 13]*
- **Latency budget table:** retain, but header MUST read
  *"Illustrative estimates — own analysis, not measured data"* until/unless Phase 2
  captures provide real figures.

---

## SECTION 6 — GOOGLE EDGE & APPLICATION PROCESSING

- **Front end:** load balancers, **TLS termination** (Google sees plaintext — trust
  implication stated plainly), **WAF**, DDoS protection.
  *[CITE: Google Cloud Armor / Cloud CDN docs]*
- **Certificate facts:** issuer, SANs, chain to a trusted root.
  *[PLACEHOLDER — reuse the single Lab 05 inspection; cite Artifact 12]*
- **Application processing + response:** request handling, generation, security headers.
  **Security+ connection:** 2.3-A/G, 2.4-C.
  **Evidence slot:** *[PLACEHOLDER — Lab 09 DVWA scan + manual verification; cite
  Artifact 16]*

---

## SECTION 7 — SECURITY THROUGHOUT *(merged; former §7 Return Path folded into §5/§6 prose)*

Four compact tables, each cell citing a lab artifact or labeled (own analysis):
**Confidentiality · Integrity · Authentication · Authorization** (per-layer protections +
evidence source). Authorization rows must include carrier ACLs (Lab 07), Google service
access control, browser sandboxing.

**Change in the System (NEW — required by Passport 1.3-B/C/D):**
Short narrative of the controlled-change cycle actually executed in Phase 2:
**Build → baseline → change → test → compare → document → restore/rollback → validate.**
Cite the change log / version-control artifacts. *(This earns 1.3-B/C/D legitimately —
do not cut this section.)*

**Attack-surface summary:** **maximum 5 rows** — component / vector / mitigation — with
pointer: *"Full map = Artifacts 7–8."*

**Where security fails:** 4 numbered realistic failure modes (CA compromise, carrier
insider, BGP hijack, endpoint compromise) — one mitigation line each.

---

## SECTION 8 — CONCLUSION

Four short labeled subsections, each ≤ 5 bullets:
1. **Why it's secure** — defense in depth (layers, authN points, isolation, monitoring, access control).
2. **Weaknesses** (metadata, DNS exposure, carrier trust, physical, endpoint).
3. **What could break** (CA compromise, route leaks, zero-days, DDoS).
4. **Evidence of compromise would look like** — per the Lab 11 methodology: unusual DNS
   queries, invalid certificates, abnormal transfers, repeated auth failures, unexpected
   file changes. *[PLACEHOLDER — cite Artifact 18]*

Close with the governing line: **"Coverage is planned. Evidence is earned. Nothing is assumed."**

---

## APPENDICES

### Appendix A — Evidence Inventory *(empty until Phase 2 — fill from executed labs only)*

| Artifact # | File | Lab | Description | Status |
|---|---|---|---|---|
| | | | | ☐ pending |

### Appendix B — Security+ Coverage Pointer *(summary row ONLY — full matrix = Artifact 22)*

| Domain | Demonstrated | Understood | Encountered | Not a target |
|---|---|---|---|---|
| 1 | *(auto from Passport)* | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |

❌ PROHIBITED: hand-typed requirement-ID lists; any total count such as "68 addressed";
promotion of Encountered items into "addressed" columns.

### Appendix C — References *(final form only — verified, actually-retrieved sources)*

☐ CompTIA SY0-701 objectives · ☐ RFC 8446 (TLS 1.3) · ☐ 3GPP TS 33.501
· ☐ Cisco 5G AMF/xHaul guides · ☐ NIST 5G security CSWP · ☐ OWASP WSTG · ☐ MDN HTTP caching

---

**Document Version:** 2.0-scaffold · **Authored at:** Mission end (Phase 3) ·
**Completion gate:** every Appendix A row filled + every citation verified + quiz-gated
coverage updates passed per the Coverage Update Guideline.