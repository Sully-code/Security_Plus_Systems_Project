## LAB 03 — DNS Investigation

### Objective

Investigate DNS resolution in detail using real command-line tools. Understand what DNS does, where queries go, what responses contain, and what evidence DNS leaves behind.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.5-C|DNS filtering|🟢 Demonstrated|DNS filtering configuration and test evidence|
|3.2-C|Secure communication|🟢 Demonstrated|DNS security analysis (plaintext vs encrypted DNS)|
|4.4-A|Monitoring tools|🟢 Demonstrated|DNS query/response capture and analysis|
|4.9-A|Log data for investigations|🟢 Demonstrated|DNS query logs preserved as evidence|
|2.4-E|Network attacks|🟢 Demonstrated|DNS manipulation scenario understood and detected|

### Prerequisites

Lab 02 complete.

### Tools

- Ubuntu Server VM (or any Linux/macOS terminal)
- Wireshark
- dig, nslookup, host (built into Linux/macOS)
- The Packet Tracer topology from Lab 02 (for comparison)

### Environment Setup

Two tracks — simulated and real:

**Track A — Simulated (Packet Tracer from Lab 02):** The DNS server and clients from Lab 02 are already configured.

**Track B — Real observation (Linux VM):** The learner's own machine performing real DNS queries against real resolvers.

### Procedure

**Step 1 — Capture a real DNS query**

1. Open Wireshark on your host machine or Linux VM.
2. Start a capture on your active network interface.
3. Apply display filter: `dns`
4. In a terminal, run: `dig www.google.com`
5. Stop the capture.
6. Save as `mission01-lab03-dns-query-real.pcapng`.

**Step 2 — Analyze the DNS query packet**

In Wireshark, examine the DNS query:

1. Find the Standard Query (Type A) packet.
2. Document:
    - Source IP (your machine)
    - Destination IP (DNS resolver — who is it?)
    - Transaction ID
    - Query name
    - Query type (A, AAAA, etc.)
3. Write down: Is this traffic encrypted? What can an observer see?

**Step 3 — Analyze the DNS response packet**

1. Find the DNS response.
2. Document:
    - Answer records returned
    - TTL values
    - Number of answers
    - Whether the response is authoritative or cached

**Step 4 — Compare with Packet Tracer DNS**

1. In the Lab 02 topology, send a simulation packet from PC0 to the DNS server.
2. Switch to Simulation Mode in Packet Tracer.
3. Filter to show DNS events.
4. Click the DNS query packet and examine the OSI layers.
5. Compare what Packet Tracer shows with what Wireshark captured. Note similarities and differences.

**Step 5 — Investigate DNS resolver chain**

From a Linux VM terminal:

`# See which resolver your machine uses cat /etc/resolv.conf # Query a specific resolver directly dig @8.8.8.8 www.google.com # Query with full trace dig +trace www.google.com # See DNS cache behavior dig www.google.com dig www.google.com # Run again — does TTL change?`

Document each command's output and explain what it reveals about the DNS resolution process.

**Step 6 — Investigate DNS over HTTPS (DoH) vs plaintext DNS**

`# Normal DNS (plaintext, observable on the wire) dig www.google.com # Compare: if your system supports DoH, investigate how it differs # Firefox settings: about:config → network.trr.mode # Document what DoH does to observability`

Write a short analysis: If DNS is plaintext, what can an attacker on the network see? What can a defender monitor? What does encrypting DNS change?

**Step 7 — DNS filtering investigation**

On the Linux VM (or in Packet Tracer using ACLs):

`# Simulate DNS filtering by blocking a specific domain resolution # On a Linux VM acting as DNS resolver: sudo apt install dnsmasq sudo nano /etc/hosts # Add: 0.0.0.0 blocked-example.test sudo systemctl restart dnsmasq # Configure your test VM to use this resolver # Then try: dig blocked-example.test @127.0.0.1`

Document what happens and how DNS filtering can serve as a security control.

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Real DNS capture (pcap)|DNS investigation evidence|
|Packet Tracer DNS simulation analysis|Part of technical report|
|DNS chain analysis document|DNS investigation evidence|
|DNS security analysis (plaintext vs DoH)|Security-control analysis|
|DNS filtering demonstration|DNS filtering evidence|

### Success Criteria

- Learner can identify the resolver IP their machine uses
- Learner can explain the difference between a DNS query and response in Wireshark
- Learner can explain why plaintext DNS is a security concern
- Learner has demonstrated DNS filtering as a security control
- PCAP evidence is saved and annotated

### Curiosity Branches

- What is DNSSEC and why does it exist? (Record under Curiosity Branches)
- How does a caching resolver reduce latency? Can you measure the difference?
- What is a DNS sinkhole and how is it used in security operations?