# MISSION 01 — LABORATORY PLAN

## Operating Framework

Every lab follows this lifecycle, derived from the Passport's operating model:

`OBJECTIVE → SETUP → PROCEDURE → OBSERVATION → ARTIFACT → SECURITY+ MAPPING`

## Tool Stack (All Free)

|Tool|Purpose|Platform|
|---|---|---|
|**Packet Tracer**|Network topology, routing, switching simulation|Windows/Mac/Linux (free via Cisco NetAcad)|
|**VirtualBox**|Virtualization host for Linux VMs|Windows/Mac/Linux|
|**Ubuntu Server 22.04 LTS**|General-purpose lab machines, DNS, web server, tools|VM guest|
|**Wireshark**|Packet capture and protocol analysis|Host or VM|
|**Nmap**|Port scanning, service discovery, vulnerability scanning|VM|
|**OpenSSL**|Certificate inspection, TLS investigation, hashing|Built into Linux/macOS|
|**dig / nslookup / host**|DNS investigation|Built into most OSes|
|**tcpdump**|Command-line packet capture|Linux VM|
|**curl**|HTTP/HTTPS requests, certificate retrieval|Built into most OSes|
|**pfSense (VM)**|Firewall, access control, DNS filtering|VirtualBox guest|
|**Suricata**|IDS/IPS signature-based detection|Linux VM|
|**OpenVAS / Greenbone**|Vulnerability scanning|Linux VM (or Docker)|
|**draw.io (diagrams.net)**|Architecture diagrams, attack-surface maps|Web browser|
|**Python 3**|Scripting, automation, log parsing|Linux VM|
|**traceroute / mtr**|Path investigation|Linux/macOS|
|**ip / ifconfig**|Interface and addressing inspection|Linux|

---

## Phase Mapping

The 12 labs fall into five progressive phases that mirror the mission's system journey:

|Phase|Labs|Journey Stage|
|---|---|---|
|**1 — Architecture & Modeling**|Lab 01, Lab 02|Understand and build the system|
|**2 — Protocol Investigation**|Lab 03, Lab 04, Lab 05|Trace the protocols end-to-end|
|**3 — Failure & Security Controls**|Lab 06, Lab 07, Lab 08|Break, defend, and distinguish failures|
|**4 — Operational Security**|Lab 09, Lab 10|Vulnerability lifecycle + monitoring|
|**5 — Investigation & Reconstruction**|Lab 11, Lab 12|Forensics and end-to-end synthesis|

---