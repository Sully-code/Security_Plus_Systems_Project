## LAB 05 — TLS Investigation

### Objective

Inspect a real TLS/HTTPS connection in detail. Understand certificate chains, trust relationships, encryption negotiation, and how confidentiality and integrity are established during the handshake.

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|1.4-A|PKI|🟢 Demonstrated|Certificate chain analysis with OpenSSL|
|1.4-B|Encryption|🟢 Demonstrated|Cipher suite negotiation documented|
|1.4-D|Hashing|🟢 Demonstrated|Certificate fingerprint hashing demonstrated|
|1.4-E|Digital signatures|🟡 Understood|Signature presence in certificates documented|
|1.2-A|Confidentiality|🟢 Demonstrated|TLS confidentiality mechanism explained from real evidence|
|1.2-B|Integrity|🟢 Demonstrated|TLS MAC/AEAD integrity mechanism documented|
|1.2-E|Authentication|🟢 Demonstrated|Server authentication via certificate explained|
|3.2-C|Secure communication|🟢 Demonstrated|TLS session establishment traced end-to-end|

### Prerequisites

Lab 04 complete.

### Tools

- OpenSSL (built into Linux/macOS)
- Wireshark (existing HTTPS capture from Lab 04)
- curl
- draw.io

### Procedure

**Step 1 — Retrieve a server's certificate with OpenSSL**

`# Connect to example.com and dump the cert echo | openssl s_client -connect example.com:443 -servername example.com 2>/dev/null | openssl x509 -text -noout`

Document the following from the certificate output:

- Issuer (who signed this certificate?)
- Subject (who is the certificate for?)
- Validity period (not before, not after)
- Public key algorithm and key size
- Signature algorithm
- SANs (Subject Alternative Names)
- Serial number

**Step 2 — Extract and compare certificate fingerprints**

`# SHA-256 fingerprint echo | openssl s_client -connect example.com:443 -servername example.com 2>/dev/null \ | openssl x509 -fingerprint -sha256 -noout # SHA-1 fingerprint (legacy — note why it's deprecated) echo | openssl s_client -connect example.com:443 -servername example.com 2>/dev/null \ | openssl x509 -fingerprint -sha1 -noout`

Document both fingerprints. Explain:

- What is a certificate fingerprint?
- Why is it hashed?
- Why is SHA-1 deprecated for this purpose?
- How does this relate to the concept of integrity?

**Step 3 — Trace the certificate chain**

`# Show the full certificate chain echo | openssl s_client -connect example.com:443 -servername example.com -showcerts 2>/dev/null`

Identify:

1. The server (leaf) certificate
2. The intermediate CA certificate
3. The root CA (if present or known)

In draw.io, create a certificate chain diagram:

`Root CA (self-signed, in your trust store) │ signs Intermediate CA │ signs Server certificate (example.com)`

Document: Why does the chain exist? What would happen if the intermediate were missing?

**Step 4 — Examine the TLS handshake from the Lab 04 capture**

Open `mission01-lab04-https-capture.pcapng` in Wireshark.

Filter: `tls.handshake`

Examine in order:

1. **Client Hello** — list cipher suites offered, TLS version, extensions (SNI, ALPN)
2. **Server Hello** — selected cipher suite, selected TLS version
3. **Certificate** — server sends its certificate chain
4. **Key exchange** — which key exchange mechanism was used?
5. **Change Cipher Spec** — what does this signal?
6. **Finished** — what is verified here?

Document the full handshake sequence with one-sentence explanations for each message.

**Step 5 — Identify what each handshake step achieves**

Fill in this table:

|Handshake Message|Security Property Achieved|
|---|---|
|Client Hello|?|
|Server Hello|?|
|Certificate|?|
|Key Exchange|?|
|Change Cipher Spec|?|
|Finished|?|

Map each to: confidentiality, integrity, authentication, or a combination.

**Step 6 — Demonstrate a trust failure**

`# Connect to a server with a self-signed or expired cert openssl s_client -connect self-signed.badssl.com:443 -servername self-signed.badssl.com`

Document:

- What error does OpenSSL report?
- Why did the connection fail?
- What would a browser show?
- What security decision is being enforced here?

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Certificate analysis document|TLS/certificate analysis|
|Certificate chain diagram (draw.io)|Trust-boundary diagram (supporting)|
|TLS handshake analysis document|TLS/certificate analysis|
|Trust failure analysis|Part of technical report|

### Success Criteria

- Learner can retrieve a server certificate using OpenSSL and identify its key fields
- Learner can explain the certificate chain and why intermediates exist
- Learner can trace the TLS handshake from a Wireshark capture
- Learner can map each handshake step to a security property (CIA triad + authentication)
- Learner can explain what happens when trust cannot be established
- Certificate chain diagram is clean and accurate

### Curiosity Branches

- What is Certificate Transparency and why was it created?
- How does Let's Encrypt issue free certificates? What does ACME stand for?
- What is Perfect Forward Secrecy and why does the key exchange matter?
- What is a certificate revocation list (CRL) vs OCSP?