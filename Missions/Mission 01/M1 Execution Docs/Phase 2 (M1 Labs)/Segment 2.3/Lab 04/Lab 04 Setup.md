
## LAB 04 — Packet Capture

### Objective

Capture, dissect, and analyze real network traffic using Wireshark. Develop the ability to identify protocols, understand packet structure, and extract investigative evidence from captured traffic.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.4-A|Monitoring tools|🟢 Demonstrated|Wireshark capture and analysis evidence|
|4.4-B|Computing resource activities|🟢 Demonstrated|Protocol behavior documented from captures|
|4.9-A|Log data for investigations|🟢 Demonstrated|Packet capture preserved as investigative evidence|
|4.9-B|Other data sources|🟢 Demonstrated|Endpoint data correlated with network captures|
|1.2-B|Integrity|🟢 Demonstrated|TCP checksum integrity observed in captures|
|3.2-C|Secure communication|🟢 Demonstrated|Protocol analysis of plaintext vs encrypted traffic|

### Prerequisites

Lab 03 complete.

### Tools

- Wireshark
- Linux VM (Ubuntu Server)
- curl
- tcpdump (optional, command-line alternative)
- Python 3 (for log parsing)

### Procedure

**Step 1 — Capture a complete HTTP request/response**

1. Start Wireshark capture on the Linux VM interface.
2. In a terminal: `curl http://example.com`
3. Stop capture.
4. Save as `mission01-lab04-http-capture.pcapng`.
5. Apply filter: `http`
6. Examine:
    - HTTP GET request packet — identify headers, Host, User-Agent
    - HTTP response packet — identify status code, content type
    - Follow TCP stream: right-click → Follow → TCP Stream. Read the full plaintext conversation.

**Step 2 — Capture a complete HTTPS request/response**

1. Start a new Wireshark capture.
2. In a terminal: `curl https://example.com`
3. Stop capture.
4. Save as `mission01-lab04-https-capture.pcapng`.
5. Apply filter: `tls or tcp`
6. Examine:
    - TLS Client Hello — what does it contain? (cipher suites, SNI extension, supported versions)
    - TLS Server Hello — what cipher suite was selected?
    - Can you read the application-layer data? Why or why not?
    - Document the exact point where plaintext ends and encryption begins.

**Step 3 — Compare HTTP and HTTPS captures**

Create a side-by-side analysis:

|Aspect|HTTP capture|HTTPS capture|
|---|---|---|
|Can you read request content?|?|?|
|Can you read response content?|?|?|
|What headers are visible?|?|?|
|What metadata is visible even in encrypted traffic?|?|?|
|What can an attacker see?|?|?|
|What can a defender monitor?|?|?|

**Step 4 — Examine the TCP three-way handshake**

From the HTTPS capture:

1. Filter: `tcp.flags.syn == 1`
2. Identify the SYN, SYN-ACK, ACK sequence.
3. Document:
    - Source and destination ports
    - Sequence numbers
    - Window size
4. Answer: Why does TCP use a three-way handshake? What security properties does it establish?

**Step 5 — Capture DNS + HTTP in a single session**

1. Start capture.
2. Run: `curl http://example.com` (fresh — no cache: `curl --no-keepalive http://example.com`)
3. Stop capture.
4. Filter: `dns or http or tcp`
5. Reconstruct the full event sequence:
    - DNS query
    - DNS response
    - TCP SYN
    - TCP SYN-ACK
    - TCP ACK
    - HTTP GET
    - HTTP response
    - TCP FIN

Write out the timeline with timestamps from the capture.

**Step 6 — Capture and analyze a traceroute**

`# From Linux VM traceroute www.google.com # or mtr www.google.com`

While running, capture with Wireshark filtered on ICMP. Document:

- How many hops are visible
- Which hops respond and which don't
- How traceroute uses TTL increments to discover the path

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|HTTP capture (pcap)|Packet captures|
|HTTPS capture (pcap)|Packet captures|
|HTTP vs HTTPS comparison table|Part of technical report|
|TCP handshake analysis|Protocol-stack diagram (supporting evidence)|
|Timeline reconstruction from combined capture|Part of incident reconstruction methodology|
|traceroute analysis|Part of technical report|

### Success Criteria

- Learner can identify DNS, TCP, and HTTP/TLS packets in a capture
- Learner can explain why HTTPS traffic is unreadable at the application layer
- Learner can explain what metadata remains visible even in encrypted traffic
- Learner can reconstruct a chronological event sequence from packet captures
- PCAPs are saved and properly annotated

### Curiosity Branches

- What is QUIC and how does it differ from TCP+TLS? (Research the protocol)
- How does Wireshark identify protocols if the traffic is encrypted?
- What is a PCAP file format and why is it the standard for network evidence?