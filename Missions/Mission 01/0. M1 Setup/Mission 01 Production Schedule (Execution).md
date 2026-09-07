## REVISED PRODUCTION SCHEDULE — PHASE 1: ARCHITECTURE (NOW)

This schedule respects the documents' philosophy while preventing "what comes next" questions. It organizes work by **journey segments**, not lab numbers, with continuous Security+ mapping and evidence tracking.

---

### OVERVIEW

|Phase|Work Type|Driving Force|Output|
|---|---|---|---|
|**Phase 1**|Architecture|Journey questions|Artifacts 1–8 + Security+ planning record|
|**Phase 2**|Investigation|Evidence gaps|Artifacts 9–20 + Learner evidence record|
|**Phase 3**|Integration|Synthesis|Artifacts 21–23 + Gap analysis|

---

### PHASE 1: ARCHITECTURE (CURRENT PHASE)

Each journey segment goes through Section 9's cycle. We produce artifacts incrementally.

| Segment | Driving Question                                                         | Architecture Work            | Security+ Mapping       | Artifacts Produced | Exit Criteria                      |
| ------- | ------------------------------------------------------------------------ | ---------------------------- | ----------------------- | ------------------ | ---------------------------------- |
| **1.1** | "When I press Enter, what is the very first thing my phone has to know?" | Level 0 → Level 1 diagrams   | 1.2-A/C/E/F, 3.2-A/C/D  | Artifact 1–2       | Level 1 diagram accepted           |
| **1.2** | "How does the phone authenticate on the carrier network?"                | Level 2 carrier architecture | 1.2-E, 4.1-B, 4.6-A     | Artifact 3–4       | Level 2 diagram + auth flow mapped |
| **1.3** | "What address does the phone actually use, and how is it assigned?"      | Addressing architecture      | 1.2-F, 2.3-C, 4.1-A     | Artifact 5–6       | IP/DNS assignment understood       |
| **1.4** | "How does google.com become an address?"                                 | DNS resolution architecture  | 1.4-A, 4.5-C, 4.9-B     | Artifact 7         | DNS flow documented                |
| **1.5** | "Where are trust boundaries in this system?"                             | Trust boundary analysis      | 1.2-D/E/H, 2.2-H, 3.2-B | Artifact 6–8       | Trust map complete                 |
| **1.6** | "Where could an attacker interfere?"                                     | Attack surface mapping       | 2.2-B/H, 2.3-G, 2.4-E   | Artifact 7–8       | Attack surface map complete        |
| **1.7** | "Which Security+ requirements does this mission actually own?"           | Coverage review              | All domains             | Artifact 22        | Planned coverage record finalized  |

**Total Phase 1 Duration:** Until artifacts 1–8 exist + Security+ planned coverage recorded.

**Exit Signal to Phase 2:** All Level 0–2 architecture diagrams accepted, trust boundaries mapped, attack surfaces documented, planned coverage finalized.

---

### PHASE 2: INVESTIGATION (NEXT PHASE)

Each lab serves a segment. Not a checklist — evidence-seeking activity.

|Segment|Lab(s)|Driving Question|Investigation Work|Evidence Collected|Security+ Demonstrated|
|---|---|---|---|---|---|
|**2.1**|Lab 01–02|"Does our simplified model actually route traffic?"|Build & test topology|Working config, routing evidence|2.5-A/B/D, 3.2-A/B|
|**2.2**|Lab 03|"What DNS queries actually occur?"|Capture DNS resolution|Packet captures, timing logs|1.4-A, 4.4-A, 4.9-A/B|
|**2.3**|Lab 04|"What does the full packet journey look like?"|Full capture investigation|Wireshark traces|4.4-A, 4.9-A/B|
|**2.4**|Lab 05|"How is trust established cryptographically?"|TLS handshake inspection|Certificate chain, key exchange logs|1.4-A/B/E, 1.2-A/B/D|
|**2.5**|Lab 06–08|"What happens when things break?"|Failure injection & analysis|Routing failure logs, DNS attack evidence|2.4-E, 4.8-C/D/F, 4.9-A/B|
|**2.6**|Lab 09–11|"Can we track a vulnerability end-to-end?"|Full lifecycle exercise|Vulnerability ID → remediation → validation → report|4.3-A-E, 4.8-A-F|
|**2.7**|Lab 12|"Can we reconstruct the journey from evidence?"|Reverse engineering from data|Timeline, root cause, affected components|4.8-D, 4.9-A/B|

**Exit Signal to Phase 3:** All labs executed, all artifacts produced, learner evidence status updated.

---

### PHASE 3: INTEGRATION (FINAL PHASE)

|Work Item|Output|Security+ Focus|
|---|---|---|
|3.1 Risk Analysis|Artifact 20|5.2-A/B/C/G|
|3.2 Mission Technical Report|Artifact 21|All domains|
|3.3 Final Security+ Coverage Record|Artifact 22|Complete matrix with actual evidence|
|3.4 Independent Journey Explanation|Artifact 23|All domains — without prepared script|

**Mission Complete When:** Artifacts 21–23 exist, learner can explain journey independently, remaining gaps assigned to later missions or Verification Labs.



Reminder: Provide snapshots at these times 
`## Artifact 1 — Level 0 Snapshot *Quick scan at diagram milestone.* ### Security+ Concepts Touched | Requirement | Status | Why | |-------------|--------|-----| | **1.2-A** Confidentiality | 🔵 Encountered | TLS/encryption mentioned | | **1.2-C** Availability | 🔵 Encountered | Multiple path failures noted | | **1.2-E** Authentication | 🟡 Understood | SIM/carrier auth explained | | **1.4-A** PKI | 🔵 Encountered | Certificate validation mentioned | | **1.4-B** Encryption | 🟡 Understood | HTTPS/TLS discussed | | **2.2-B** Unsecure network vectors | 🔵 Encountered | DNS manipulation risk noted | | **2.2-H** Attack surfaces | 🔵 Encountered | Each hop as potential attack surface | | **3.2-A** Infrastructure considerations | 🟡 Understood | Major components mapped | | **4.5-C** DNS filtering | 🔵 Encountered | DNS as security control point | ### Evidence Earned? **None yet.** This is architecture/hypothesis. Labs produce evidence in Phase 2. ### What Comes Next? Level 1 diagram will touch more concepts (routing, trust boundaries, carrier infrastructure). --- **Snapshot Rule:** I only do this when you complete an artifact or ask for it. No chatter between milestones.`