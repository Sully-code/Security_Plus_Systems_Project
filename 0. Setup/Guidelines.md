## ✅ Rule: All Labs Must Be 100% Free to Complete

|Constraint|Applied To|
|---|---|
|No paid software required|✅ GNS3, Packet Tracer, Wireshark (all free)|
|No paid hardware required|✅ No RTL-SDR, no Starlink terminal, no enterprise gear|
|Research-only labs permitted|✅ As long as source materials are free (ITU, FCC, public benchmarks)|
|Documentation/diagramming allowed|✅ [draw.io](http://draw.io/), Lucidchart free tier, pen + paper|
|Optional hardware purchases|✅ OK if learner chooses (not required for Security+ coverage)|

---

## Program Artifacts

> **Passport** — What will this mission investigate, build, test, document, and ultimately produce?

> **Atlas Register** — How does this mission fit into the overall nine-mission program, and what Security+ knowledge does it own/share?

> **Portfolio** — The actual artifacts produced when the missions are completed.

---

## Coverage Update Guideline

> Before a Security+ coverage update is given, I must be quizzed on what we covered for anything labeled **Understood** and up (or for every requirement in that segment). We'll go over it, so technically everything should be understood — but we'll base the chart on my initial answers rather than my understanding after the review.

---

## Citation Standard Going Forward

Every technical claim must include:

> `Claim Statement [(Source Name)](URL)` — exact/paraphrased quote from source — section/clause reference — why this supports the claim

**Example of the expected format:**

> Tower (gNodeB) is just a relay — it doesn't validate credentials [(3GPP TS 23.501, Clause 6.2.3)](upload required): _"The gNB does not perform authentication; it acts as a radio access node forwarding NAS messages between the UE and the AMF."_ — This means the authentication logic lives in the core network (AUSF/UDM), not at the radio tower.

---

## Standing Requirements

|Claim Type|Sourcing Requirement|
|---|---|
|Technical architecture (5GC functions, interfaces)|3GPP specs (uploaded)|
|Security controls (firewalls, WAF, encryption)|NIST / OWASP / vendor docs|
|Security+ requirements|CompTIA materials only|
|Own analysis / reasoning|No citation needed|

---

## Verification Notes

|Citation|Why It's Valid|
|---|---|
|MDN Web Docs|Mozilla's official developer documentation, maintained by web standards experts|
|Cloudflare CDN|Industry-leading CDN provider's educational content|
|Imperva HTTP Keep-Alive|Security/CDN vendor's technical documentation|
|Cisco Routing|Official Cisco learning materials for networking fundamentals|

## Search Discipline

|When Searching for Citations|Do This|Don't Do This|
|---|---|---|
|General networking concepts (routing, caching)|Find **concept explanation**, not tangential articles|Don't grab any article with the keyword|
|Technical architecture (5GC functions)|Use **specification documents** (3GPP, Cisco configs)|Don't use blog posts or summaries|
|Security principles (TLS, encryption)|Use **standards bodies** (IETF, NIST, OWASP)|Don't force unrelated security articles|

> **Never try to force a citation that doesn't match or make sense.**

---

## Proposed Citation Framework (Reputable Sources Only)

Exhaust **Option B** and **Option C** first before asking for **Option A**. The focus is accuracy — so if needed, ask directly for Option A.

### Option A — Upload the Spec Documents _(best for accuracy)_

Download and upload the actual specifications; I then parse them directly and quote/paraphrase with exact clause references.

`Documents to upload: ├── 3GPP TS 33.501 (5G Security Architecture) — authentication/authentication vector details ├── 3GPP TS 23.501 (5G System Architecture) — network function definitions ├── RFC 8446 (TLS 1.3) — TLS handshake details └── Google Security Whitepapers — edge infrastructure controls`

### Option B — Web-Extract from Authoritative HTML Pages _(good balance)_

|Source|URL|What I Can Extract|
|---|---|---|
|**RFC Editor**|[https://www.rfc-editor.org/rfc/rfc8446.html](https://www.rfc-editor.org/rfc/rfc8446.html)|Full TLS 1.3 spec (HTML)|
|**IETF**|Various IETF RFCs|Protocol standards|
|**OWASP**|[https://owasp.org/www-project-web-security-testing-guide/](https://owasp.org/www-project-web-security-testing-guide/)|Security controls|
|**NIST**|[https://csrc.nist.gov/](https://csrc.nist.gov/)|Security frameworks|

### Option C — Vendor Documentation _(verified human-written, limited but usable)_

|Vendor|Type|URL|
|---|---|---|
|Cisco|Technical documentation|[https://www.cisco.com/c/en/us/products/](https://www.cisco.com/c/en/us/products/)|
|Palo Alto Networks|Security research|[https://www.paloaltonetworks.com/resources](https://www.paloaltonetworks.com/resources)|
|NIST Special Publications|Standards|[https://csrc.nist.gov/publications](https://csrc.nist.gov/publications)|

---

## Citation Placement Guidelines

|Type of Claim|Citation Needed?|Example|
|---|---|---|
|Technical architecture (network functions)|✅ Yes|AUSF, UDM, PCF names|
|Interface definitions (N1, N8, N12)|✅ Yes|"N12 — Reference point between AUSF and AMF"|
|Security principles (TLS, mutual auth)|✅ Yes|OWASP TLS statements|
|Own analysis / reasoning|❌ No|"This is different than carriers because…"|
|General concepts (routing, DNS)|❌ No|Common networking knowledge|

---

## Document Roles

> **Passport** = how to build a mission. **Atlas** = how the missions fit together. **Coverage map** = how Security+ is accounted for.