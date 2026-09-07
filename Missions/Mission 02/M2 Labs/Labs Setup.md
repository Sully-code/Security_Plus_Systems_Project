# MISSION 02 — LABORATORY PLAN

## Operating Framework

Same lifecycle as Mission 01, adapted for the research-heavy nature of satellite systems:

`RESEARCH → DOCUMENT → MODEL → COMPARE → ANALYZE → EVIDENCE → SECURITY+ MAPPING`

## Tool Stack (All Free)

|Tool|Purpose|Platform|
|---|---|---|
|**draw.io (diagrams.net)**|Architecture diagrams, threat models, timelines|Web browser|
|**Packet Tracer**|Simplified network topology modeling|Windows/Mac/Linux|
|**Web browser**|Research (FCC filings, ITU docs, SpaceX public pages, academic papers)|Any|
|**Ookla Speedtest**|Public satellite performance benchmark data|Web browser|
|**Starlink public resources**|starlink.com/technology, starlink.com/updates, progress reports|Web browser|
|**starlink.sx / satellite trackers**|Public constellation visualization|Web browser|
|**Wireshark**|Protocol analysis (comparison with Mission 01 captures)|Host/VM|
|**Python 3**|Data parsing, latency calculation, log analysis|Linux VM|
|**Markdown / text editor**|Reports and documentation|Any|

---

## Phase Mapping

|Phase|Labs|Journey Stage|
|---|---|---|
|**1 — Architecture & Modeling**|Lab 01, Lab 02|Understand and model the satellite system|
|**2 — Security Investigation**|Lab 03, Lab 04|RF link security and physical infrastructure|
|**3 — Resilience & Performance**|Lab 05, Lab 06, Lab 07|Availability, failure modes, diagnostics|
|**4 — Threat & Risk**|Lab 08, Lab 09|Threat modeling and regulatory landscape|
|**5 — Synthesis**|Lab 10|End-to-end comparative reconstruction|

---

## Key Constraint Note

Mission 02 is inherently more research-oriented than Mission 01. The free-tool rule applies strictly — no Starlink terminal purchase is required. Where hands-on testing isn't possible (launching satellites, operating RF equipment), labs use public data, simulation, and documentation. The Passport explicitly permits research-only labs as long as source materials are free (FCC, ITU, public benchmarks).