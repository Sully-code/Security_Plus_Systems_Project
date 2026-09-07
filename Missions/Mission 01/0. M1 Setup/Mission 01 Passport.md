# Security+ Mission Atlas — Mission 01

# SECURITY+ MISSION ATLAS

## MISSION PASSPORT

**MISSION:** 01 — How Does My Phone Reach Google?  
**VERSION:** 2.0 — Final Architecture Baseline  
**STATUS:** Designed / Not Executed  
**DESTINATION:** CompTIA Security+ V7

---

# 1. DESTINATION

**CompTIA Security+ V7**

The mission is a vehicle for demonstrating Security+ knowledge.

It is not a substitute for the Security+ requirements.

The Security+ requirements are maintained independently in the Atlas Sub-Element Requirements Matrix.

Mission 01 is responsible for accounting for every atomic requirement and identifying what level of coverage the mission is expected to provide.

---

# 2. MISSION INTENT

Understand the complete end-to-end journey of information from a mobile device to an Internet service and back.

The mission begins with a deceptively simple question:

> **What actually happens when I type `[google.com](http://google.com/)` into my phone while driving past a cell tower?**

The objective is not merely to learn cellular networking.

The objective is to develop the ability to:

- trace information through a complex system
    
- identify the components involved
    
- understand how devices communicate
    
- understand how identities are established
    
- understand how information is protected
    
- understand how information is addressed and routed
    
- identify trust boundaries
    
- identify attack surfaces
    
- identify security controls
    
- analyze failures
    
- investigate evidence
    
- understand dependencies
    
- modify a system safely
    
- deliberately break portions of a system
    
- determine why they failed
    
- apply mitigations
    
- explain the entire system coherently
    
- map demonstrated knowledge to Security+
    

Security+ concepts will be introduced when they become necessary to answer questions about the system.

---

# 3. SCENARIO

You are using a smartphone while traveling down a highway.

You open a browser and enter:

`[https://www.google.com/](https://www.google.com/)`

You press Enter.

Within moments, Google responds.

The mission is to reconstruct what happened.

We want to understand the journey from:

**Human → Application → Phone → Radio → Cellular Network → Carrier Core → Internet → Google → Response**

at progressively deeper levels.

---

# 4. END STATE

Mission 01 is complete when the learner can independently:

1. Draw the major architecture involved in the journey.
    
2. Trace the request from application to destination and the response back.
    
3. Explain the major roles of the cellular radio network, transport network, carrier core, Internet, and destination infrastructure.
    
4. Explain addressing and name resolution at the relevant levels.
    
5. Explain the major protocols involved.
    
6. Explain where authentication and authorization occur.
    
7. Explain how confidentiality and integrity are established.
    
8. Explain the role of certificates and PKI.
    
9. Identify meaningful trust boundaries and attack surfaces.
    
10. Identify relevant security controls.
    
11. Analyze selected failure scenarios.
    
12. Investigate actual network evidence where practical.
    
13. Build a simplified representation of the system.
    
14. Deliberately break portions of the simplified system.
    
15. Explain the resulting behavior.
    
16. Apply appropriate mitigations.
    
17. Investigate evidence following a simulated security event.
    
18. Perform root-cause analysis on selected failures.
    
19. Map the demonstrated knowledge back to Security+ atomic requirements.
    
20. Identify which Security+ requirements remain outside the mission's ownership.
    
21. Produce tangible evidence of learning.
    
22. Deliver a coherent **"Phone → Google" systems narrative** without relying on a prepared script.
    

---

# 5. WHY THIS MISSION EXISTS

This is the foundational systems mission of the Atlas.

A single web request crosses multiple technological domains:

- mobile computing
    
- wireless communications
    
- networking
    
- switching
    
- routing
    
- addressing
    
- DNS
    
- transport protocols
    
- application protocols
    
- encryption
    
- authentication
    
- PKI
    
- security controls
    
- carrier infrastructure
    
- Internet infrastructure
    
- cloud/edge infrastructure
    
- physical infrastructure
    
- monitoring
    
- investigation
    

That makes it an unusually efficient learning vehicle.

It also establishes a recurring pattern for the entire Atlas:

> **Something happens → trace the system → identify dependencies → identify trust → identify threats → build a model → break it → defend it → investigate it → explain it.**

---

# 6. SYSTEM ARCHITECTURE

The architecture will be explored through multiple zoom levels.

## LEVEL 0 — Human View

```
PHONE
  ↓
INTERNET
  ↓
GOOGLE
  ↓
WEBPAGE
```

At this level the goal is simply to establish the journey.

---

## LEVEL 1 — Major System View

```
Smartphone
    ↓
Cellular Radio Network
    ↓
Carrier Network
    ↓
Internet
    ↓
Google Infrastructure
    ↓
Response
```

Questions introduced:

- What is the cellular radio network?
    
- What is the carrier network?
    
- Where does the Internet begin?
    
- What exactly is "Google" from a networking perspective?
    

---

## LEVEL 2 — Network Architecture

```
┌───────────────┐
│ Smartphone    │
└───────┬───────┘
        │
      5G NR
        │
        ▼
┌───────────────┐
│ gNodeB / RAN  │
└───────┬───────┘
        │
    Transport
        │
        ▼
┌───────────────┐
│ Carrier Core  │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│ IP Network /  │
│ Internet      │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│ Google / Edge │
│ Infrastructure│
└───────────────┘
```

This is a conceptual architecture rather than a claim that every carrier implements the exact same physical topology.

---

## LEVEL 3 — Protocol View

The journey becomes a stack of interacting protocols and services.

```
Application
    │
HTTPS
    │
TLS
    │
TCP / QUIC
    │
IP
    │
Link / Ethernet / Cellular
    │
Physical / Radio
```

Alongside the primary flow:

```
Identity
Authentication
Authorization
DNS
Address Assignment
Routing
Security Controls
Logging / Monitoring
```

The precise protocol path will be investigated rather than assumed.

---

## LEVEL 4 — Infrastructure View

We zoom into actual components and interfaces.

Potential components include:

- smartphone modem
    
- antennas
    
- radio access equipment
    
- gNodeB
    
- transport links
    
- routers
    
- switches
    
- carrier core functions
    
- firewalls/security systems
    
- DNS infrastructure
    
- Internet routers
    
- peering/transit infrastructure
    
- Google edge infrastructure
    
- application servers/services
    

The mission does not require reproducing a real carrier network.

The goal is understanding the functions and relationships.

---

## LEVEL 5 — Evidence View

We now ask:

> **What evidence would prove that this actually happened?**

Potential evidence:

- DNS queries
    
- IP addresses
    
- packet captures
    
- TCP/QUIC behavior
    
- TLS handshakes
    
- certificate information
    
- routing information
    
- interface information
    
- logs
    
- timestamps
    
- connection states
    
- firewall events
    
- IDS/IPS events
    
- endpoint/network metadata
    
- vulnerability findings
    
- failure behavior
    

---

# 7. SYSTEM JOURNEY

The canonical journey we will eventually be able to explain is:

```
USER
 ↓
BROWSER
 ↓
SMARTPHONE OS
 ↓
NETWORK STACK
 ↓
CELLULAR MODEM
 ↓
5G RADIO
 ↓
gNodeB / RAN
 ↓
CARRIER TRANSPORT
 ↓
5G CORE
 ↓
CARRIER IP NETWORK
 ↓
INTERNET
 ↓
GOOGLE EDGE / SERVICE
 ↓
GOOGLE APPLICATION INFRASTRUCTURE
 ↓
RESPONSE
 ↓
RETURN PATH
 ↓
PHONE
 ↓
BROWSER
```

However, the journey will not be treated as one monolithic process.

It will be decomposed into questions and evidence.

---

# 8. CORE QUESTIONS

## Application

- What does the browser actually do?
    
- What happens when `[google.com](http://google.com/)` is entered?
    
- How does the phone determine what service it is contacting?
    
- What application protocols are involved?
    

## Naming

- What is DNS?
    
- How does `[google.com](http://google.com/)` become an address?
    
- Where does the DNS request go?
    
- What protects DNS?
    
- What happens if DNS is manipulated?
    

## Addressing

- What address does the phone have?
    
- Is it globally routable?
    
- What addresses exist at different layers?
    
- Where does NAT occur, if applicable?
    
- How does address assignment work?
    

## Cellular

- How does the phone communicate with the tower?
    
- What is 5G NR?
    
- What is a gNodeB?
    
- How does the phone select a cell?
    
- What happens while the phone is moving?
    
- How does cellular identity work?
    
- Where does cellular authentication occur?
    

## Carrier Network

- What happens after the radio signal reaches the tower?
    
- How does traffic travel through the carrier?
    
- What is the transport network?
    
- What is the carrier core?
    
- Where are identity and mobility functions involved?
    
- How is traffic separated?
    

## Routing

- How does traffic find its destination?
    
- What routers make decisions?
    
- What is a routing table?
    
- What happens when a route disappears?
    
- How can routing failures be distinguished from security-policy failures?
    

## Transport

- What is TCP?
    
- When is UDP used?
    
- Where does QUIC fit?
    
- What does a connection actually mean?
    
- How do loss and latency affect the application?
    

## Security

- Where does authentication happen?
    
- Where does authorization happen?
    
- How is confidentiality established?
    
- How is integrity protected?
    
- What does a certificate prove?
    
- What is PKI?
    
- Where are trust boundaries?
    
- Where could an attacker interfere?
    
- What security controls can be placed at each layer?
    

## Availability

- What happens if a link fails?
    
- What happens if a router fails?
    
- What happens if DNS becomes unavailable?
    
- What happens if the cellular connection changes?
    
- How does the system recover?
    
- What evidence identifies the failure?
    

## Evidence

- What can we observe?
    
- What can Wireshark show?
    
- What can logs show?
    
- What can vulnerability data show?
    
- What can we infer?
    
- What can we not prove from available evidence?
    

---

# 9. MISSION OPERATING MODEL

Mission 01 follows this cycle:

```
QUESTION
   ↓
ARCHITECTURE
   ↓
INVESTIGATION
   ↓
MODEL
   ↓
IMPLEMENTATION
   ↓
OBSERVATION
   ↓
FAILURE / ATTACK / CHANGE
   ↓
EVIDENCE
   ↓
MITIGATION
   ↓
VALIDATION
   ↓
EXPLANATION
   ↓
SECURITY+ MAPPING
```

The mission should not become a sequence of disconnected textbook lessons.

Each concept should enter because the system creates a reason to understand it.

---

# 10. SECURITY+ COVERAGE MODEL

## Coverage rule

Every Security+ atomic requirement must appear in the Atlas.

No requirement disappears because it does not fit Mission 01.

Mission 01 does not need to own every requirement.

It does need to account for every requirement.

The coverage status in this passport represents the **expected level of coverage by the time Mission 01 is complete**.

It does **not** represent current learner achievement.

---

## Coverage status vocabulary

|Status|Meaning|
|---|---|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) **Demonstrated**|Mission 01 is expected to produce practical evidence of the requirement.|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) **Understood**|Mission 01 is expected to produce explanation/application evidence, but not necessarily deep implementation.|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) **Encountered**|Mission 01 is expected to place the requirement in meaningful context, but deeper mastery belongs elsewhere.|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) **Not a Mission 01 Target**|The requirement is accounted for in the Atlas but deliberately not owned by Mission 01.|

These colors are **planned completion coverage**, not current status.

They must not be interpreted as evidence already earned.

---

# 11. SECURITY+ ATOMIC COVERAGE

## DOMAIN 1 — GENERAL SECURITY CONCEPTS

### 1.1 — Security Controls

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.1-A** Compare technical controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.1-B** Compare preventive controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.1-C** Compare managerial controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.1-D** Compare deterrent controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.1-E** Compare operational controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.1-F** Compare detective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.1-G** Compare physical controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.1-H** Compare corrective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.1-I** Compare compensating controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.1-J** Compare directive controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

**Mission evidence:** security-control analysis, firewall/access-control work, monitoring, failure scenarios, physical/security architecture analysis, corrective and compensating control discussion.

---

### 1.2 — Fundamental Security Concepts

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.2-A** Summarize confidentiality|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.2-B** Summarize integrity|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.2-C** Summarize availability|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.2-D** Explain non-repudiation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.2-E** Explain authentication|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.2-F** Explain authorization|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.2-G** Explain accounting|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.2-H** Explain Zero Trust|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.2-I** Explain deception/disruption technology|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

---

### 1.3 — Change Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.3-A** Explain business processes associated with change management|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**1.3-B** Explain technical implications of changes|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.3-C** Explain change documentation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.3-D** Explain/use version control|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

**Required scenario:**

> **Build → baseline → change → test → compare → document → rollback/version**

This prevents change management from becoming an artificial checkbox.

---

### 1.4 — Cryptographic Solutions

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**1.4-A** Use/understand PKI|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.4-B** Use/understand encryption|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.4-C** Understand obfuscation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**1.4-D** Use/understand hashing|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**1.4-E** Use/understand digital signatures|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**1.4-F** Understand blockchain|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|

---

# DOMAIN 2 — THREATS, VULNERABILITIES & MITIGATIONS

## 2.1 — Threat Actors and Motivations

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.1-A** Compare nation-state threat actors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.1-B** Compare unskilled attackers|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.1-C** Compare hacktivists|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.1-D** Compare insider threats|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.1-E** Compare organized crime|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.1-F** Understand shadow IT as a threat/risk|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.1-G** Understand data exfiltration motivation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.1-H** Understand espionage motivation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.1-I** Understand financial gain motivation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

---

## 2.2 — Threat Vectors and Attack Surfaces

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.2-A** Explain message-based vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.2-B** Explain unsecure network vectors|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.2-C** Explain social engineering vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.2-D** Explain file-based vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.2-E** Explain voice call vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.2-F** Explain supply chain vectors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.2-G** Explain vulnerable software vectors|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.2-H** Identify/analyze relevant attack surfaces|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

**Required artifact:**

> **Actual attack-surface / threat-vector map**

The mission must distinguish theoretical attack surfaces from attacks actually reproduced.

---

## 2.3 — Vulnerabilities

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.3-A** Explain application vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.3-B** Explain hardware vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.3-C** Explain mobile device vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.3-D** Explain virtualization vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**2.3-E** Explain OS-based vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.3-F** Explain cloud-specific vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.3-G** Explain web-based vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.3-H** Explain supply chain vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

---

## 2.4 — Malicious Activity

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.4-A** Analyze malware attacks|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.4-B** Analyze password attacks|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.4-C** Analyze application attacks|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.4-D** Analyze physical attacks|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**2.4-E** Analyze network attacks|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.4-F** Analyze cryptographic attacks|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

**Principle:**

> Analyze does not mean safely reproduce every attack.

Offensive activities remain controlled and confined to authorized laboratory environments.

---

## 2.5 — Mitigation Techniques

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**2.5-A** Apply segmentation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.5-B** Apply access control|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.5-C** Apply configuration enforcement|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.5-D** Apply hardening|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.5-E** Apply isolation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**2.5-F** Apply patching|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

**Pressure-test conclusion:** this remains one of Mission 01's strongest practical areas.

---

# DOMAIN 3 — SECURITY ARCHITECTURE

## 3.1 — Architecture Models

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.1-A** Compare on-premises architecture|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**3.1-B** Compare cloud architecture|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**3.1-C** Compare virtualization architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**3.1-D** Compare IoT architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**3.1-E** Compare ICS architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**3.1-F** Compare Infrastructure as Code|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

Mission 01 encounters and distinguishes these models.

It does not pretend to own their deep implementation.

---

## 3.2 — Enterprise Infrastructure

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.2-A** Apply security principles to infrastructure considerations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**3.2-B** Apply security principles to control selection|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**3.2-C** Apply security principles to secure communication|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**3.2-D** Apply security principles to secure access|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

**Pressure-test conclusion:** very strong natural fit.

---

## 3.3 — Data Protection

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.3-A** Compare relevant data types|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**3.3-B** Compare data securing methods|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**3.3-C** Understand general data protection considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**3.3-D** Apply data classifications|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

---

## 3.4 — Resilience and Recovery

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**3.4-A** Explain high availability|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**3.4-B** Explain site considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**3.4-C** Explain testing for resilience/recovery|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**3.4-D** Explain power considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**3.4-E** Explain platform diversity|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**3.4-F** Explain backups|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**3.4-G** Explain continuity of operations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

Mission 01 establishes resilience reasoning; deeper recovery belongs elsewhere.

---

# DOMAIN 4 — SECURITY OPERATIONS

## 4.1 — Computing Resources

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.1-A** Apply secure baselines|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.1-B** Apply security to mobile solutions|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.1-C** Apply hardening|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.1-D** Apply wireless security|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.1-E** Apply application security|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.1-F** Apply sandboxing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.1-G** Apply monitoring to computing resources|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

---

## 4.2 — Asset Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.2-A** Manage hardware/software/data acquisition|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.2-B** Manage asset disposal|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**4.2-C** Manage asset assignment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.2-D** Manage asset monitoring/tracking|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

Mission 01 establishes the concepts; lifecycle ownership belongs elsewhere.

---

## 4.3 — Vulnerability Management

This receives full lifecycle treatment.

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.3-A** Identify vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.3-B** Analyze vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.3-C** Remediate vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.3-D** Validate remediation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.3-E** Report vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

### Required evidence

> **Identify → Analyze → Remediate → Validate → Report**

A vulnerability scanner alone does not satisfy 4.3.

---

## 4.4 — Alerting and Monitoring

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.4-A** Explain/use monitoring tools|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.4-B** Explain computing resource activities relevant to monitoring|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

---

## 4.5 — Enterprise Security

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.5-A** Modify/configure firewalls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.5-B** Use/configure IDS/IPS|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.5-C** Use/configure DNS filtering|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.5-D** Use/configure DLP|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.5-E** Use/configure NAC|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.5-F** Use/configure EDR/XDR|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

Mission 01 must not artificially implement every enterprise security technology merely to generate a checkbox.

---

## 4.6 — Identity and Access Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.6-A** Implement provisioning|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.6-B** Implement SSO|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.6-C** Implement MFA|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.6-D** Implement/use privileged access tools|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

Authentication and authorization are strong Mission 01 concepts, but Mission 01 is not the primary IAM implementation mission.

---

## 4.7 — Automation and Orchestration

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.7-A** Explain automation use cases|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.7-B** Explain scripting benefits|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.7-C** Explain automation considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

Automation may support evidence collection, network analysis, configuration, and reporting without becoming the mission's central subject.

---

## 4.8 — Incident Response

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.8-A** Implement incident response processes|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.8-B** Address incident response training|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**4.8-C** Conduct incident response testing|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.8-D** Perform root cause analysis|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.8-E** Conduct threat hunting|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**4.8-F** Conduct/use digital forensics|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

Mission evidence comes from:

- failure reconstruction
    
- controlled security scenarios
    
- evidence preservation
    
- investigation
    
- timeline reconstruction
    
- root-cause analysis
    
- controlled incident-response testing
    

---

## 4.9 — Data Sources

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**4.9-A** Use log data to support investigations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**4.9-B** Use other data sources to support investigations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|

Potential evidence includes:

- firewall logs
    
- application logs
    
- endpoint/OS logs
    
- IDS/IPS logs
    
- network logs
    
- metadata
    
- vulnerability scans
    
- automated reports
    
- dashboards
    
- packet captures
    
- certificate information
    
- DNS evidence
    
- timestamps
    

---

# DOMAIN 5 — SECURITY PROGRAM MANAGEMENT & OVERSIGHT

## 5.1 — Security Governance

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.1-A** Understand guidelines|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.1-B** Understand policies|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.1-C** Understand standards|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.1-D** Understand procedures|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.1-E** Understand external considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.1-F** Understand monitoring within governance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.1-G** Understand governance structures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.1-H** Understand roles/responsibilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

---

## 5.2 — Risk Management

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.2-A** Perform/understand risk identification|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**5.2-B** Perform/understand risk assessment|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**5.2-C** Perform/understand risk analysis|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**5.2-D** Maintain/use a risk register|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.2-E** Understand risk tolerance|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.2-F** Understand risk appetite|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.2-G** Select/apply risk strategies|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|
|**5.2-H** Perform risk reporting|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.2-I** Conduct/use a BIA|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

Risk is legitimate where the mission requires decisions about system exposure, controls, failure consequences, and mitigation.

Mission 01 is not the primary enterprise risk-management mission.

---

## 5.3 — Third-Party Risk

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.3-A** Conduct vendor assessment|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.3-B** Conduct vendor selection|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.3-C** Understand/manage vendor agreements|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.3-D** Conduct vendor monitoring|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.3-E** Use vendor questionnaires|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.3-F** Establish/use rules of engagement|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|

Mission 01 deliberately does not manufacture third-party-risk coverage.

---

## 5.4 — Security Compliance

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.4-A** Understand compliance reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.4-B** Understand consequences of non-compliance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.4-C** Conduct compliance monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.4-D** Understand/apply privacy considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

---

## 5.5 — Audits and Assessments

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.5-A** Understand attestation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.5-B** Understand/participate in internal audits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.5-C** Understand/participate in external audits|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.5-D** Understand/use penetration testing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

---

## 5.6 — Security Awareness

|Atomic requirement|Mission 01 completion coverage|
|---|---|
|**5.6-A** Implement phishing training|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target|
|**5.6-B** Recognize anomalous behavior|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|
|**5.6-C** Provide user guidance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.6-D** Implement user reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|
|**5.6-E** Implement/use monitoring|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|

---

# 12. COVERAGE INTEGRITY RESULT

The pressure test produces the following architectural conclusion:

## The Atlas is complete.

Every atomic Security+ requirement is accounted for.

## Mission 01 is not expected to demonstrate every requirement.

That is intentional.

Mission 01's responsibility is to:

1. demonstrate the requirements naturally supported by the Phone → Google system;
    
2. establish meaningful understanding of adjacent requirements;
    
3. deliberately encounter requirements whose deeper treatment belongs elsewhere;
    
4. explicitly identify requirements that are not Mission 01 targets.
    

This prevents false coverage.

---

# 13. COVERAGE CLASS DEFINITIONS

## ![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated

Mission 01 must produce practical evidence.

Typical evidence:

- working configuration
    
- packet capture
    
- system diagram
    
- controlled failure
    
- remediation
    
- validation
    
- investigation
    
- reconstructed behavior
    
- functioning security control
    
- technical report
    

---

## ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood

Mission 01 must produce explanation/application evidence.

The learner must be able to explain the concept and apply it to the system.

---

## ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered

Mission 01 places the requirement into meaningful context.

The learner should recognize the concept and understand why it exists, but deeper mastery belongs elsewhere.

---

## ![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 01 Target

The requirement remains in the Atlas but Mission 01 deliberately does not own it.

No artificial lab should be created merely to change the color.

---

# 14. CONCEPTS TO DISCOVER

These are not a chapter list.

They are the conceptual territory expected to emerge while answering mission questions.

## Networking

- Ethernet
    
- switching
    
- routing
    
- IP addressing
    
- subnetting
    
- NAT
    
- DHCP
    
- DNS
    
- TCP
    
- UDP
    
- QUIC
    
- HTTP/HTTPS
    
- routing tables
    
- peering/transit
    

## Cellular

- RF
    
- 5G NR
    
- RAN
    
- gNodeB
    
- spectrum
    
- cells
    
- mobility
    
- handover
    
- cellular identity
    
- SIM/eSIM
    
- carrier core
    
- transport network
    

## Security

- authentication
    
- authorization
    
- accounting
    
- encryption
    
- hashing
    
- digital signatures
    
- certificates
    
- PKI
    
- TLS
    
- trust boundaries
    
- Zero Trust
    
- firewalls
    
- IDS/IPS
    
- DNS filtering
    
- monitoring
    
- vulnerability management
    
- incident response
    
- digital forensics
    

## Infrastructure

- fiber
    
- routers
    
- switches
    
- network interfaces
    
- data centers
    
- edge infrastructure
    
- power
    
- timing
    
- physical security
    

---

# 15. LABS

**Important:** These are planned labs. Nothing is considered executed merely because it appears here.

## Lab 01 — Build the Simplified Journey

Create:

```
Client
  ↓
Access Network
  ↓
Carrier/ISP Router
  ↓
Internet
  ↓
Web Server
```

Goal:

Understand the basic packet journey before adding complexity.

---

## Lab 02 — Build the Carrier-Like Network

Expand the model:

```
Client
   ↓
Access Network
   ↓
Aggregation
   ↓
Regional Router
   ↓
ISP Core
   ↓
Internet
   ↓
Destination
```

Introduce:

- interfaces
    
- addressing
    
- routing
    
- segmentation
    
- failure points
    
- security controls
    

---

## Lab 03 — DNS Investigation

Investigate:

```
Application
    ↓
DNS Query
    ↓
Resolver
    ↓
DNS Response
    ↓
Destination Address
```

Evidence:

- DNS queries
    
- responses
    
- addresses
    
- timing
    
- filtering behavior
    

---

## Lab 04 — Packet Capture

Use Wireshark or an equivalent controlled capture environment.

Investigate:

- packet structure
    
- addressing
    
- transport
    
- DNS
    
- TLS/QUIC behavior
    
- timing
    
- connection states
    

---

## Lab 05 — TLS Investigation

Inspect a real or controlled HTTPS connection.

Investigate:

- certificates
    
- certificate chains
    
- trust
    
- encryption
    
- authentication
    
- integrity
    
- TLS negotiation
    
- digital signatures
    

---

## Lab 06 — Routing Failure

Deliberately remove or disable a route in the simulated environment.

Observe:

- loss of connectivity
    
- routing behavior
    
- convergence
    
- alternate paths where configured
    
- evidence of failure
    

---

## Lab 07 — Firewall / Access Control

Implement controlled security policies.

Ask:

> What traffic should be allowed, denied, logged, or inspected?

Then test the policy.

---

## Lab 08 — DNS Attack Scenario

Within the isolated lab, model a DNS manipulation scenario.

Investigate:

- what changes
    
- what evidence appears
    
- what security control could detect/prevent it
    
- how the user experience changes
    

---

## Lab 09 — Vulnerability Lifecycle

Introduce a controlled vulnerability into the lab.

Complete:

```
IDENTIFY
   ↓
ANALYZE
   ↓
REMEDIATE
   ↓
VALIDATE
   ↓
REPORT
```

This lab exists specifically to prevent 4.3 from being reduced to "run a scanner."

---

## Lab 10 — Monitoring and Investigation

Generate controlled activity and investigate it using multiple evidence sources.

Correlate:

- logs
    
- packet captures
    
- timestamps
    
- network metadata
    
- endpoint information
    
- security-tool output
    

---

## Lab 11 — Incident Reconstruction

Given evidence rather than a diagram, reconstruct what happened.

Produce:

- timeline
    
- affected components
    
- root cause
    
- evidence supporting the conclusion
    
- security controls involved
    
- recommended remediation
    

---

## Lab 12 — End-to-End Reconstruction

Given evidence rather than a diagram, reconstruct the complete Phone → Google journey.

This becomes one of the first true systems-engineering exercises.

---

# 16. FAILURE SCENARIOS

## Failure A — DNS unavailable

> Can the user reach the destination if name resolution fails?

---

## Failure B — Route disappears

> What happens when the preferred path disappears?

---

## Failure C — Firewall rule blocks traffic

> How do we distinguish a security-policy failure from a network failure?

---

## Failure D — Cellular connectivity changes

> What happens when the phone moves between cells?

---

## Failure E — High latency

> How do we determine where latency was introduced?

---

## Failure F — Packet loss

> How does packet loss affect the application?

---

## Failure G — Certificate/trust failure

> What happens when the client cannot establish trust?

---

## Failure H — Vulnerable component discovered

> How do we identify, analyze, remediate, validate, and report the vulnerability?

---

## Failure I — Suspicious network activity

> Can we reconstruct what happened from available evidence?

---

# 17. ATTACK SCENARIOS

The architecture will consider:

- rogue/unauthorized wireless infrastructure
    
- DNS manipulation
    
- credential theft
    
- malicious network traffic
    
- application vulnerabilities
    
- man-in-the-middle concepts
    
- denial/disruption
    
- physical compromise
    
- insecure configuration
    
- vulnerable software
    

The distinction between:

**attack concept → safe simulation → actual reproduction**

will be maintained throughout the Atlas.

Offensive activities remain controlled and authorized.

---

# 18. TANGIBLE ARTIFACTS

Mission 01 will ultimately produce:

1. **Level 0 architecture diagram**
    
2. **Level 1 architecture diagram**
    
3. **Level 2 carrier architecture**
    
4. **Detailed packet-flow diagram**
    
5. **Protocol-stack diagram**
    
6. **Trust-boundary diagram**
    
7. **Attack-surface map**
    
8. **Threat-vector map**
    
9. **Simplified network topology**
    
10. **DNS investigation evidence**
    
11. **Packet captures**
    
12. **TLS/certificate analysis**
    
13. **Routing-failure analysis**
    
14. **Firewall/security-policy configuration**
    
15. **Security-control analysis**
    
16. **Vulnerability lifecycle evidence**
    
17. **Monitoring evidence**
    
18. **Incident reconstruction**
    
19. **Root-cause analysis**
    
20. **Risk analysis**
    
21. **Mission 01 technical report**
    
22. **Security+ atomic coverage record**
    
23. **Final "Phone → Google" explanation**
    

The final explanation is itself an artifact.

---

# 19. EVIDENCE OF LEARNING

The learner's **actual state** is tracked separately from the passport's **planned completion coverage**.

The Atlas status vocabulary remains:

|Status|Meaning|
|---|---|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png)|Not encountered|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Encountered|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Understood|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Demonstrated|
|![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png)|Exam verified|

The passport's coverage table does **not** pre-award these states.

For example:

> A requirement marked ![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) in the passport means Mission 01 is designed to produce demonstration evidence.

It does **not** mean the learner has already demonstrated it.

The actual Atlas record changes only when evidence exists.

---

# 20. SECURITY+ COVERAGE VS. LEARNER STATE

This distinction is mandatory.

### Passport

Answers:

> **What should Mission 01 cover by completion?**

### Atlas evidence record

Answers:

> **What has the learner actually demonstrated?**

Therefore:

```
PLANNED MISSION COVERAGE
        ≠
CURRENT LEARNER EVIDENCE
```

A mission can be designed to demonstrate something and still have zero evidence because the mission has not been executed.

---

# 21. FAILURE / ATTACK / CHANGE DISCIPLINE

Every deliberate modification should follow a controlled cycle:

```
BASELINE
   ↓
CHANGE
   ↓
OBSERVE
   ↓
DOCUMENT
   ↓
ANALYZE
   ↓
RESTORE
   ↓
VALIDATE
```

Security incidents follow a related cycle:

```
EVENT
   ↓
PRESERVE EVIDENCE
   ↓
INVESTIGATE
   ↓
RECONSTRUCT
   ↓
ROOT CAUSE
   ↓
MITIGATE
   ↓
VALIDATE
   ↓
REPORT
```

This gives Mission 01 legitimate connections to change management, vulnerability management, monitoring, incident response, forensics, and risk.

---

# 22. OPEN QUESTIONS

The following questions should drive the investigation:

1. What exactly happens between pressing Enter and the DNS request?
    
2. Where does DNS resolution occur?
    
3. What address does the phone actually use?
    
4. How does the phone attach to the cellular network?
    
5. What does the gNodeB actually do?
    
6. What happens inside the carrier transport network?
    
7. What does the 5G core do?
    
8. Where does authentication occur?
    
9. How is the user's traffic separated from other users?
    
10. Where does routing occur?
    
11. Where does NAT occur, if applicable?
    
12. How does traffic reach the Internet?
    
13. How does Google receive the traffic?
    
14. How does HTTPS establish trust?
    
15. What does the certificate prove?
    
16. Where does encryption begin?
    
17. What happens if a router fails?
    
18. What happens if DNS fails?
    
19. What happens if the cellular connection changes?
    
20. What evidence can we capture?
    
21. Which Security+ controls are actually visible?
    
22. Which Security+ concepts remain only theoretical?
    
23. Which concepts require targeted verification labs?
    
24. What evidence would distinguish a network failure from a security control failure?
    
25. What evidence would allow reconstruction of an event after the fact?
    
26. How can a discovered vulnerability be tracked through remediation?
    
27. How can we validate that a mitigation actually worked?
    

---

# 23. CURIOSITY BRANCHES

Potential branches include:

## Cellular

- 5G NR
    
- spectrum
    
- antennas
    
- beamforming
    
- gNodeB architecture
    
- handovers
    
- SIM/eSIM
    
- cellular authentication
    
- carrier core
    

## Infrastructure

- fiber optics
    
- SFPs
    
- timing
    
- GPS/PTP
    
- tower equipment
    
- power systems
    
- batteries
    
- environmental monitoring
    
- microwave backhaul
    

## Networking

- BGP
    
- OSPF
    
- MPLS
    
- carrier Ethernet
    
- Internet exchange points
    
- peering
    
- transit
    
- CDN architecture
    

## Security

- TLS
    
- PKI
    
- certificate authorities
    
- DNSSEC
    
- encrypted DNS
    
- Zero Trust
    
- mobile security
    
- rogue base stations
    
- IDS/IPS
    
- DNS filtering
    
- endpoint security
    

## Google

- edge networks
    
- CDNs
    
- load balancing
    
- distributed systems
    
- data centers
    
- service architecture
    

---

# 24. DEFERRED TOPICS

These are intentionally captured rather than allowed to derail the mission.

Initial candidates:

- detailed BGP route-selection mechanics
    
- deep 5G radio engineering
    
- orbital/satellite networking
    
- advanced optical transport
    
- detailed carrier-core implementation
    
- Google's private internal infrastructure
    
- advanced timing protocols
    
- blockchain
    
- advanced cryptographic mathematics
    
- deep enterprise IAM
    
- deep vendor management
    
- enterprise audit mechanics
    
- detailed DLP implementation
    
- detailed NAC implementation
    
- detailed EDR/XDR implementation
    

A deferred topic can become active if it becomes necessary to answer a mission question.

Otherwise it remains deferred.

---

# 25. PRESSURE-TEST FINDINGS

The revised system journey is particularly strong for:

- security controls
    
- CIA
    
- authentication
    
- authorization
    
- cryptography
    
- network security
    
- attack surfaces
    
- vulnerabilities
    
- mitigation
    
- secure communication
    
- secure access
    
- mobile security
    
- application security
    
- secure baselines
    
- hardening
    
- wireless security
    
- monitoring
    
- vulnerability management
    
- firewall/DNS controls
    
- evidence collection
    
- packet analysis
    
- incident investigation
    
- root-cause analysis
    
- data sources
    
- risk analysis
    

The journey provides legitimate context for many other Security+ concepts without pretending to be their primary mission.

---

# 26. WHAT THE PRESSURE TEST REJECTED

Mission 01 will **not** artificially expand itself to demonstrate:

- blockchain
    
- deep cloud vulnerability implementation
    
- deep virtualization vulnerability implementation
    
- deep supply-chain implementation
    
- DLP implementation
    
- NAC implementation
    
- EDR/XDR implementation
    
- vendor management
    
- vendor questionnaires
    
- external audits
    
- attestation
    
- BIA
    
- deep governance structures
    
- phishing-training implementation
    
- advanced radio engineering
    
- Google's private internal architecture
    

These remain represented in the Atlas and can be owned by other missions or targeted Security+ Verification Labs.

---

# 27. NEXT MISSION CONNECTIONS

Mission 01 is intentionally foundational.

It establishes vocabulary and systems reasoning that later missions can reuse without reteaching the underlying concepts from scratch.

Potential connections include:

### Mission 02 — Starlink

Extends:

- wireless communications
    
- satellite networking
    
- routing
    
- distributed infrastructure
    
- resilience
    
- availability
    
- physical security
    
- alternative communication paths
    

### Mission 03 — Secure Innovation Lab

Extends:

- network architecture
    
- segmentation
    
- access control
    
- firewalls
    
- monitoring
    
- secure baselines
    
- vulnerability management
    

### Mission 06 — Drone ISR

Extends:

- wireless
    
- mobility
    
- secure communications
    
- availability
    
- authentication
    
- resilience
    

Mission 01 therefore acts as a foundational systems vocabulary builder without becoming a prerequisite for every later mission.

---

# 28. CURRENT STATE

**Mission status:** Not started.

**Architecture status:** Defined at conceptual level.

**Security+ coverage design:** Pressure-tested.

**Atomic requirements:** All accounted for.

**Planned completion coverage:** Defined.

**Labs:** Designed, not executed.

**Artifacts:** None produced yet.

**Security+ evidence:** None yet.

**Learner state:** Not pre-awarded.

---

# 29. WHAT WE KNOW

At mission launch, we know the intended architecture and learning objectives.

We do **not** assume that understanding the architecture on paper constitutes demonstrated knowledge.

The mission begins with the question.

---

# 30. WHAT WE HAVE BUILT

The mission architecture and learning design have been built.

The laboratory implementation has not.

The first implementation artifact will be the simplified representation of the journey.

---

# 31. NEXT RECOMMENDED ACTION

**Do not configure anything yet.**

First establish the **Level 0 → Level 1 architecture together** and identify the first unknowns.

The first question remains:

> **When I press Enter on `[google.com](http://google.com/)`, what is the very first thing my phone has to know or do before it can send the request toward Google?**

That question determines the first conceptual branch of the mission.

---

# 32. MISSION COMPLETE WHEN

Mission 01 is complete only when:

- the end-to-end architecture can be drawn
    
- the system journey can be explained
    
- the major protocols can be explained
    
- the major trust relationships can be explained
    
- relevant Security+ concepts can be applied
    
- selected traffic can be investigated
    
- the simplified system has been built
    
- selected failures have been introduced
    
- security controls have been applied
    
- evidence has been analyzed
    
- vulnerabilities have been taken through an appropriate lifecycle
    
- selected incidents have been reconstructed
    
- root causes have been identified
    
- tangible artifacts have been produced
    
- the learner can explain the complete journey independently
    
- Security+ atomic evidence has been recorded
    
- remaining gaps have been identified
    
- unresolved Security+ gaps have been assigned to later missions or Verification Labs
    

---

# 33. HANDOFF NOTES FOR ANOTHER AI

**Do not restart this mission from scratch.**

The learner is using a systems-journey learning model.

The destination is **CompTIA Security+ V7**.

The mission is **Mission 01 — How Does My Phone Reach Google?**

The learner prefers understanding systems by tracing real events end-to-end rather than studying concepts in arbitrary textbook order.

Do not turn this into a generic networking course.

Do not introduce Packet Tracer or other execution prematurely.

The mission begins in the **architecture phase**.

The next useful action is to investigate the first step of the journey and progressively refine the architecture.

When a concept is encountered, map it to the Security+ atomic matrix.

When a concept is expected to be demonstrated, require evidence before awarding the corresponding learner status.

When curiosity creates a valuable but nonessential branch, record it under **Curiosity Branches** or **Deferred Topics**.

Do not mark an objective demonstrated merely because the passport says the mission is designed to demonstrate it.

Do not expand Mission 01 with new major activities solely to turn an inconvenient Security+ requirement green.

Use a targeted **Security+ Verification Lab** when necessary.

The governing principle remains:

> **Security+ is the destination. The Mission Atlas is the vehicle.**

---

# 34. ARCHITECTURAL FREEZE

This version incorporates the final pressure-test decisions.

The following are considered **frozen design principles** for the Atlas unless deliberately reopened:

1. **Every Security+ atomic requirement remains represented in the Atlas.**
    
2. **Mission passports use atomic Security+ coverage rather than separate parent-level coverage.**
    
3. **Mission coverage represents intended coverage by mission completion, not current learner achievement.**
    
4. **Coverage uses four planning classes: Demonstrated, Understood, Encountered, Not a Mission Target.**
    
5. **Actual learner evidence uses the separate five-state Atlas vocabulary: ![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png).**
    
6. **Mission ownership is not the same thing as Atlas coverage.**
    
7. **A mission is not expanded artificially to accommodate poorly fitting objectives.**
    
8. **Verification Labs are legitimate mechanisms for closing Security+ gaps.**
    
9. **4.8 Incident Response and 4.9 Data Sources remain separate objectives.**
    
10. **Labs are planned until actually executed.**
    
11. **Artifacts are not considered produced until they actually exist.**
    
12. **A future AI should use this passport as the authoritative Mission 01 design rather than reconstructing the mission from conversation history.**
    

---

## FINAL GOVERNING PRINCIPLE

> **Security+ is the destination.**
> 
> **The Mission Atlas is the vehicle.**
> 
> **The missions are real systems to investigate, build, break, defend, and explain.**
> 
> **Coverage is planned. Evidence is earned. Nothing is assumed.**