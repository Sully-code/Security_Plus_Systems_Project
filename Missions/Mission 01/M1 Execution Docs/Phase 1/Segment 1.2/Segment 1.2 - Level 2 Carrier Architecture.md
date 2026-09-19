# **Driving Question:** "How does the phone authenticate on the carrier network?"

---

## **PLAN 1a — Home Network Authentication**

### **My Initial Mental Model:**

- This happens when the phone first turns on / mobile data is turned on. The phone connection travels through the tower RAN to the carrier network.
- The phone sends the carrier the private and public key, the carrier identifies it through the public key.
- The carrier authenticates the connection and gives it a temporary identity with the network.
- The carrier forwards the connection through the trust boundary to the public network / internet where it continues its journey.

#### **Initial Model Accuracies**

|My Guess|Real Engineering Parallel|
|---|---|
|Happens when phone turns on / mobile data enabled|This triggers the **Registration Request** — the UE (User Equipment, your phone) asks to join the network [(3GPP TS 33.501, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "When a UE registers with the PLMN for the first time, the network performs a primary authentication of the UE."|
|Connection travels through tower / RAN to carrier|The **gNodeB** (the 5G cell tower) is a relay — it forwards signaling (**NAS** messages) from the UE to the AMF (Access and Mobility Management Function) in the core, but doesn't make authentication decisions [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "The N2 reference point between R(AN) and AMF carries NAS signaling."|
|Carrier identifies the phone|The phone sends its identity to the network — either as **SUCI** (Subscription Concealed Identifier, the encrypted SUPI) or **5G-GUTI** (temporary identity) if previously allocated [(3GPP TS 33.501, Clause 6.1.1.4)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to the core network."|
|Carrier gives it a temporary identity|After successful authentication, the AMF allocates a **5G-GUTI** (Globally Unique Temporary Identity) so the phone doesn't have to send its permanent identity again [(ETSI TS 133 501 V16.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.13.00_60/ts_133501v161300p.pdf): "the UE should send the SEAF a temporary identifier (a 5G-GUTI) or an encrypted permanent identifier (a SUCI) if a 5G-GUTI has not been allocated."|
|Eventually forwards through trust boundary to internet|Correct in the big picture, though this is a **separate** step from authentication. Authentication establishes identity and keys; establishing a data session (**PDU session**) that actually carries traffic to the Internet is a subsequent process [(3GPP TS 33.501, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "PDU session establishment requires prior registration / authentication completion."|

##### **Acronym Glossary — Initial Model Accuracies Table**

- **UE (User Equipment)** = Your phone or any device that connects to the 5G network
    
- **3GPP (3rd Generation Partnership Project)** = The organization that writes all the rules and technical standards for cellular networks (2G, 3G, 4G, 5G)
    
- **PLMN (Public Land Mobile Network)** = The carrier's network itself — basically Verizon, AT&T, T-Mobile's infrastructure
    
- **NAS (Non-Access Stratum)** = The signaling protocol between your phone and the core network (things like 'register me,' 'authenticate me,' 'start a data session'). It's called 'non-access' because these messages are addressed to the core network functions and are **transparently relayed** by the radio tower (gNodeB) — the gNodeB forwards them without reading or modifying their contents
    
- **RAN (Radio Access Network)** = Everything that handles the radio connection: cell towers, antennas, and the equipment that turns your phone's wireless signal into something the core network can understand
    
- **AMF (Access and Mobility Management Function)** = The network function that handles registration, authentication, and mobility (handoffs when you move). Think of it as the "gatekeeper" that decides if your phone is allowed to connect and keeps track of where you are
    
- **SUCI (Subscription Concealed Identifier)** = Your encrypted ID. Your phone's permanent identity gets encrypted before it ever goes over the air, so eavesdroppers can't read it
    
- **SUPI (Subscription Permanent Identifier)** = Your actual permanent subscriber ID (basically the 5G version of an IMSI). It's stored on your SIM and in the carrier's database. In 5G, this is always encrypted as SUCI when sent over the air
    
- **GUTI (Globally Unique Temporary Identity)** = A temporary ID the network assigns to you after authentication. Instead of sending your real ID every time, you send this temporary ID to protect your privacy
    
- **SEAF (Security Anchor Function)** = A security component that sits between the radio network and the authentication server. In practice, it's co-located with the AMF, so you usually don't hear about it separately
    

---

#### **Corrections to Initial Model**

|My Words|Accurate Framing|Why It Matters for Sec+|
|---|---|---|
|"Phone sends the carrier the private and public key"|**The SIM never sends its secret key.** The SIM stores a long-term shared secret **K** (symmetric key, not a public / private key pair). K exists in two places: on the SIM and in the carrier's UDM/ARPF. It is **never transmitted.** [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "K: The root key, a long-term shared symmetric key stored in the UDM/ARPF and the UE's USIM."|This is the difference between symmetric and asymmetric crypto. The authentication uses **challenge-response** with a shared secret, not public key exchange.|
|"Carrier identifies it through the public key"|The phone's permanent identity (**SUPI**) is encrypted using the home network's public key, producing the **SUCI** (concealed identifier). The carrier's UDM/ARPF decrypts SUCI back to SUPI. But the _authentication itself_ uses K via challenge-response — the public key is for **identity privacy**, not authentication. [(ETSI TS 133 501 V16.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.13.00_60/ts_133501v161300p.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to CN."|Two separate crypto operations are happening: **asymmetric encryption** protects identity in transit; **symmetric challenge-response** proves the SIM knows K.|
|(Missing)|**Mutual authentication** — the phone authenticates the network too, not just the network authenticating the phone. The network sends **AUTN** (authentication token), and the SIM verifies it. Only then does the SIM respond with **RES*** (its response to the challenge). [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "USIM validates AUTN using the shared secret K, computes RES*… The 5G-AKA procedure ensures mutual authentication of the UE and the serving network."|Security+ covers mutual authentication. This is also a trust boundary — the phone needs to verify it's talking to a legitimate network, not a rogue base station (IMSI catcher).|
|(Missing)|**Key derivation hierarchy** — after authentication succeeds, K seeds a tree of derived keys: **K_AUSF → K_SEAF → K_AMF → K_gNB**. Different keys protect different layers (radio link, NAS signaling, user plane). [(ETSI TS 133 501 V17.13.0, Annex A.6)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "The AUSF derives K_SEAF from K_AUSF using the serving network name as input."|Security+ tests understanding of layered key management and why deriving separate keys for separate purposes matters.|

##### **Acronym Glossary — Corrections Table**

- **K (Long-Term Secret Key)** = A secret number stored on your SIM card AND in the carrier's database (UDM/ARPF). Both sides have the same one, and it's used to prove you're who you say you are. The key itself is **never sent over the air** — instead, both sides do math with it and compare results
    
- **UDM (Unified Data Management)** = The carrier's database that holds all your subscriber information, including your secret key K. This is where the carrier "knows" who you are
    
- **ARPF (Authentication Credential Repository and Processing Function)** = The specific function _inside_ the UDM that stores K and generates authentication vectors. Think of it as the safe inside the vault — UDM is the building, ARPF is the vault [(ETSI TS 133 501 V19.6.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/19.06.00_60/ts_133501v190600p.pdf): "The UDM/ARPF shall first generate an authentication vector..."
    
- **USIM (Universal Subscriber Identity Module)** = The actual chip on your SIM card that stores your secret key K. It's the hardware that does the crypto calculations for authentication
    
- **SUPI (Subscription Permanent Identifier)** = Your permanent subscriber ID (like a username for the carrier). In 5G, this is encrypted before sending over the air to protect privacy
    
- **SUCI (Subscription Concealed Identifier)** = Your SUPI after it's been encrypted. Think of it as "your real name wrapped in an envelope that only the home carrier can open"
    
- **AUTN (Authentication Token)** = A code the network sends to your phone to prove _it_ is legitimate. If your phone can't verify the AUTN, it knows it might be talking to a fake tower (rogue base station)
    
- **RES*** = The number your phone computes using the secret key K and a random challenge from the network. The asterisk denotes the 5G-specific transformed response (different from 4G EPS-AKA's plain RES)
    
- **5G-AKA (5G Authentication and Key Agreement)** = The actual protocol name for how 5G phones authenticate. "AKA" means both sides prove they know the secret without sending the secret itself
    
- **K_AUSF (Key for Authentication Server Function)** = The first session key derived after authentication. It's the "root" for all other keys that follow
    
- **K_SEAF (Key for Security Anchor Function)** = A derived key used as the anchor for the serving network security context
    
- **K_AMF (Key for Access and Mobility Management Function)** = A derived key used to protect NAS signaling messages (registration, authentication commands, etc.)
    
- **K_gNB (Key for Next Generation NodeB)** = A derived key used to encrypt the actual radio link between your phone and the tower
    
- **AUSF (Authentication Server Function)** = The network function that actually runs the authentication procedure. It talks to the UDM/ARPF to get credentials, sends challenges to the phone, and verifies responses
    
- **gNB (Next Generation NodeB)** = The 5G version of a cell tower / base station. It handles the radio connection but doesn't make authentication decisions
    
- **SEAF (Security Anchor Function)** = A security component that acts as the bridge between the radio network and the authentication server. Usually co-located with the AMF
    

---

##### **Quick Reference — Why the Key Hierarchy Matters**

|Derived Key|What It Protects|
|---|---|
|K_AUSF|Root session key — created by the auth server (AUSF); the ancestor of every key that follows|
|K_SEAF|Bridge key handed to the serving network (held by the SEAF, co-located with the AMF)|
|K_AMF|NAS signaling — registration, authentication commands, mobility messages|
|K_gNB|Radio link — encrypts the actual wireless traffic between your phone and the tower|

---

##### **The Actual 5G-AKA Flow (Simplified)**

Here's the corrected chronology for what happens during authentication:

1. Phone turns on → wants to join the carrier network
2. Phone sends a "register me" request to the cell tower (gNB) → forwarded to the gatekeeper (AMF) - Request includes your encrypted ID (SUCI) or temporary ID (5G-GUTI) from last time
3. Gatekeeper (AMF) asks the auth server (AUSF) to verify you - Includes your encrypted ID and which serving network is involved (SNN — Serving Network Name)
4. Auth server asks the subscriber database (UDM/ARPF) for your credentials
5. Database **(UDM/ARPF/SIDF)** decrypts your ID, looks up your secret key K, and generates a challenge package - Random number (RAND), auth token (AUTN), expected answer *(XRES)**, anchor key (K_AUSF)
6. Challenge sent back to your phone: "Here's a random number and proof we're legitimate"
7. Your phone's **USIM** checks the auth token (proves we're a real network), then computes the answer using the secret key K **(mutual auth)** and derives **RES***
8. Phone sends answer (RES*) back up the chain to the auth server (AUSF)
9. Visited network **(SEAF / AMF)** hashes RES* + RAND and compares against HXRES* (local check)
10. Auth server (AUSF) compares your answer (RES*) against the expected one (XRES*) → match = you're in (home network's independent check)
11. Keys are generated for both sides independently from K: **K → CK/IK → K_AUSF → K_SEAF → K_AMF** → final keys for NAS, RRC, and user-plane encryption
12. After authentication completes and registration continues, the network may assign a new **5G-GUTI** for future use _(note: GUTI assignment is part of the broader registration procedure, not strictly part of 5G-AKA itself)_
13. You're authenticated and have security keys

**Key insight for Security+:** The secret K never leaves the SIM or the UDM/ARPF. Instead, the network sends a random challenge (RAND), and both sides independently compute a response using K. If the responses match, both sides have proven they know K without ever transmitting it. This is classic **challenge-response authentication** — a Security+ staple. Additionally, the home network performs an independent verification of the UE's response — a 5G improvement over 4G that prevents a compromised visited network from falsifying authentication results [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf).

###### **Technical Reference (Full Terminology)**

- **5G-GUTI (5G Globally Unique Temporary Identity)** = Same as GUTI from the earlier glossary, just with "5G-" in front. It's your temporary ID the network assigns after authentication so you don't have to keep sending your real identity
    
- **SNN (Serving Network Name)** = The **standardized serving network identifier** used in key derivation and authentication procedures. This is a formal identifier bound into the KDF to ensure keys generated for one serving network won't work on another [(ETSI TS 133 501 V17.13.0, Clause 6.1.1.4)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "The serving network name is constructed as specified in clause 6.1.1.4 and used in KSEAF derivation."
    
- **ARPF (Authentication Credential Repository and Processing Function)** = The part of the UDM that actually stores the secret key K and runs the crypto math. Think of it as the vault inside the UDM — the UDM is the building, the ARPF is the safe [(ETSI TS 133 501 V19.6.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/19.06.00_60/ts_133501v190600p.pdf): "The UDM/ARPF generates the 5G HE AV."
    
- **RAND (Random Challenge)** = A random number the network generates and sends to your phone. Your phone uses K to do math with RAND and produce RES*. The randomness ensures every authentication is unique and can't be replayed
    
- **XRES*** = The **Expected Response** computed by the UDM/ARPF using K. The asterisk indicates the 5G-AKA transformed value (different from 4G EPS-AKA's XRES). Your phone computes RES* the same way. If they match, authentication succeeds [(ETSI TS 133 501 V17.13.0, Figure 6.1.3.2-1)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf)
    
- **Authentication Vector (5G HE AV)** = A package of values the UDM/ARPF generates for 5G-AKA: RAND, AUTN, XRES*, and K_AUSF. The network sends RAND and AUTN to your phone as a challenge, holds XRES* to check your answer, and K_AUSF becomes the root for all session keys [(ETSI TS 133 501 V16.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.13.00_60/ts_133501v161300p.pdf)
    

---

## **PLAN 1b — Roaming (Visited Network) Authentication**

### **My Initial Mental Model:**

- The phone is handed off to a new carrier by a handoff command from the previous tower
- Assuming data is not handed off from the last tower (if the scenario is the known tower handing off to the foreign tower rather than turning the phone on and connecting directly to a foreign tower), the phone sends that tower a registration request
- The gNodeB transports that to the AMF at the core along with the encrypted identity
- The AMF forwards that to the necessary server, which forwards to a database to check for your credentials
- However, in this case your credentials aren't found unless forwarded from the home carrier
- At this point the foreign carrier would cross-talk with the phone's native carrier (database) for credential information, or either let the native tower handle the credential confirmation
- This way the identity is decrypted
- Once this is done, authentication has to probably be settled in a similar way — the native carrier may get the calculation that involves K from the native carrier, or transfer the connection in some way to be done through the native carrier
- The phone would generate its package that affirms it knows K as well, and both would generate their follow-on keys to maintain secure relationship, negating more need of the native carrier
- Then requests can be pushed to the public routing

#### **Initial Model Accuracies**

|Your Guess|Real Engineering Parallel|
|---|---|
|Phone sends registration request; gNodeB transports to AMF with encrypted identity|Same as home network — the **UE** sends a **Registration Request** with **SUCI** (or **5G-GUTI**), the visited **gNodeB** relays it to the visited **AMF** [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "A roaming UE starts registration or service in a visited network and must be authenticated against home-network credentials."|
|Credentials aren't found locally — need to contact home carrier|The visited network has no subscriber database for you. The visited **AMF** must request authentication support from the home network's **AUSF** [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "In a roaming case the visited network can no longer authenticate a subscriber on its own; the home network must be involved and must confirm the outcome."|
|Foreign carrier cross-talks with the phone's native carrier|The visited AMF contacts the home **AUSF** through inter-network gateways called **SEPPs** (Security Edge Protection Proxies). The AUSF acts as a proxy to the home **UDM/ARPF**, which holds your credentials [(3GPP TS 33.501)](https://www.3gpp.org/news-events/3gpp-news/sec-5g): "In the roaming architecture, the home and the visited network are connected through SEcurity Protection Proxy (SEPP) for the control plane of the internetwork interconnect."|
|Identity is decrypted|The **SUCI** is decrypted back to **SUPI** by the home network's **UDM** (specifically a function called **SIDF** — Subscription Identifier De-concealing Function inside the UDM). The visited network never sees the SUPI [(ETSI TS 133 501 V19.6.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/19.06.00_60/ts_133501v190600p.pdf): "Given SUCI, SIDF will de-conceal it. UDM sends 5G HE AV and SUPI to AUSF in the response."|
|Authentication settled using K; phone affirms it knows K|The challenge-response still uses **K** via **5G-AKA** — the home **UDM/ARPF** generates **RAND**, **AUTN**, and **XRES*** using K, the phone's **USIM** verifies **AUTN** (mutual auth) and computes **RES*** [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "Both UE and home network share a long-term secret key. Network creates a random number challenge RAND. Using the secret key and RAND, it computes an expected response XRES*."|
|Both generate follow-on keys; native carrier no longer needed|After authentication succeeds, the home **AUSF** derives **K_SEAF** from **K_AUSF** and sends it to the visited network. The visited network then derives **K_AMF** and **K_gNB** locally — no further home involvement needed for session keys [(ETSI TS 133 501 V17.13.0, Annex A.6)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "K_AUSF never leaves the home network. Even in roaming scenarios, the visited AMF only receives K_SEAF."|
|Eventually requests pushed to public routing|After a **PDU session** is established (separate from authentication), traffic flows through the visited network to the Internet — same as home, just routed through visited infrastructure|

##### **Acronym Glossary — Initial Model Accuracies Table**

- **SEPP (Security Edge Protection Proxy)** = A security gateway that sits at the border between two carrier networks. When the visited network and home network need to talk, all their signaling traffic passes through SEPPs on both sides. Think of it as a customs checkpoint for inter-carrier communications — it filters, protects, and authenticates the connection between the two networks
    
- **SIDF (Subscription Identifier De-concealing Function)** = The specific function inside the home network's UDM that decrypts SUCI back to SUPI. Think of it as the only person with the key to the envelope your phone sends — nobody else in the visited network can open it
    
- **5G HE Authentication Vector (Home Environment AV)** = The full package the home UDM/ARPF generates: RAND, AUTN, XRES*, and K_AUSF. This never leaves the home network intact — the AUSF transforms it before sending anything to the visited network
    
- **5G SE Authentication Vector (Serving Environment AV)** = The trimmed-down package the AUSF sends to the visited network: RAND, AUTN, HXRES*, and K_SEAF. Notice K_AUSF and XRES* are NOT included — the visited network gets hashed versions (HXRES*) instead, so it can verify the phone's response without seeing the original values
    
- **HXRES*** (Hashed Expected Response) = A hash of XRES* and RAND. The AUSF creates this so the visited network can check whether the phone's response (RES*) is correct, without ever seeing the real XRES*. It's like giving someone the answer key to a hash but not the actual answer
    
- **NRF (Network Repository Function)** = A directory service inside the 5G core. When the visited AMF needs to find the home AUSF, it (or the AUSF) can query the NRF to look up the right address — like a phone book for network functions
    

---

#### **Corrections to Initial Model**

|My Words|Accurate Framing|Why It Matters for Sec+|
|---|---|---|
|"Phone is handed off to a new carrier by a tower command"|Inter-carrier handover exists, but the more common roaming scenario is the phone registering fresh on a visited network (turning on abroad, losing home coverage). Either way, the visited network must authenticate you from scratch — a handoff command doesn't transfer trust between carriers [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "Start state: UE is attached to a visited network but is not yet trusted for secure roaming service."|Trust doesn't transfer between organizations. Each carrier maintains its own trust domain — relevant to Zero Trust (1.2-H) and trust boundary analysis.|
|"AMF forwards to the necessary server which forwards to database"|More precisely: visited **AMF** → (through **SEPP**) → home **AUSF** → home **UDM/ARPF**. The AUSF is the authentication proxy; the UDM/ARPF holds K and generates the challenge package [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "The authentication procedure begins with the AMF in the visited network requesting authentication parameters from the AUSF in the home network. This is passed through the SEPPs on the edge of each of the core networks."|Understanding the chain of custody for authentication requests — who sees what, and where the sensitive operations happen — maps to secure access (3.2-D) and infrastructure considerations (3.2-A).|
|"Cross-talk with the phone's native carrier for credential information"|The visited network **never receives K**. The home UDM/ARPF generates the **5G HE Authentication Vector** (RAND, AUTN, XRES*, K_AUSF) and sends only the **5G SE Authentication Vector** (RAND, AUTN, HXRES*, K_SEAF) to the visited network. K stays in the home network [(ETSI TS 133 501 V17.13.0, Annex A.6)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "K_AUSF never leaves the home network. Even in roaming scenarios, the visited AMF only receives K_SEAF."|This is layered key management and least-privilege design — the visited network gets exactly what it needs to serve you, and nothing more. Maps to cryptographic solutions (1.4-A/B) and access control (2.5-B).|
|"Or either let the native tower handle the credential confirmation"|The home network doesn't delegate authentication to a "native tower." Instead, the home **AUSF** verifies the UE's response (**RES*** vs **XRES***) independently. This is a 5G improvement over 4G — the home network gets final confirmation that authentication succeeded [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "5G takes security one step further in the authentication procedure when the home network receives the UE response from the visited network to authenticate independently of the visited network's authentication."|Home-network confirmation prevents a compromised visited network from falsely claiming you authenticated. Relevant to non-repudiation (1.2-D) and Zero Trust (1.2-H).|
|"Phone generates its package that affirms it knows K"|The phone doesn't initiate — it **responds to a challenge**. The flow is: network sends RAND + AUTN → phone verifies AUTN (proves network legitimacy) → phone computes RES* using K + RAND → phone sends RES* back [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "UE verifies that AUTN is valid. It then computes RES* and sends this back to the home network."|Same challenge-response principle as home auth, but the chain of relay is longer. The phone can't tell (and shouldn't care) whether it's roaming — the SIM just does crypto with what it receives.|

---

##### **Acronym Glossary — Corrections Table**

- **K_AUSF** = The root session key derived during authentication. Critically: **this key never leaves the home network**, even in roaming. The visited network never sees it [(ETSI TS 133 501 V17.13.0, Annex A.6)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "K_AUSF never leaves the home network. Even in roaming scenarios, the visited AMF only receives K_SEAF."
    
- **K_SEAF** = The key the AUSF derives from K_AUSF and hands to the visited network. This is the highest key the visited network ever gets — everything downstream (K_AMF, K_gNB) is derived from it locally
    
- **SNN (Serving Network Name)** = The **standardized serving network identifier** bound into the key derivation formula. This means keys generated for one visited network won't work on a different one. This prevents a compromised visited network from using your keys elsewhere [(ETSI TS 133 501 V17.13.0, Clause 6.1.1.4)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "This ensures that for authentication to be successful, the visited network requesting authentication vectors from the home network must be the same network that the device is actually connected to during the authentication procedure."
    
- **Home Network Confirmation** = A 5G-specific improvement where the home AUSF independently verifies the UE's response (RES* vs XRES*) rather than trusting the visited network's verdict. In 4G, the visited network did all verification — 5G adds home-network oversight [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf)
    

---

##### **Quick Reference — What the Visited Network Gets vs. Doesn't Get**

|The Visited Network Receives|The Visited Network Never Sees|
|---|---|
|RAND + AUTN (to challenge the phone)|K (the long-term secret key)|
|HXRES* (hashed expected response, to verify the phone's answer)|XRES* (the real expected response)|
|K_SEAF (to derive local session keys)|K_AUSF (the root session key)|
|SUPI (only after authentication succeeds)|The private key used to decrypt SUCI|

---

##### **The Actual 5G-AKA Flow (Roaming — Simplified)**

1. Phone arrives on visited network → sends **Registration Request** with **SUCI** (or **5G-GUTI** if previously assigned) to the visited **gNodeB**
2. Visited **gNodeB** forwards the request to the visited **AMF** (just like home — the tower is still just a relay)
3. Visited **AMF** sees it doesn't have credentials for this subscriber → sends an authentication request to the home **AUSF** (through **SEPPs** on both sides)
4. Home **AUSF** receives the request (includes your SUCI and the **SNN** — Serving Network Name of the visited carrier)
5. Home **AUSF** forwards the request to the home **UDM/ARPF**
6. Home **UDM/ARPF** decrypts **SUCI** → recovers **SUPI** → looks up your secret key **K** → generates the **5G HE Authentication Vector**: RAND, AUTN, XRES*, K_AUSF
7. Home **AUSF** receives the HE AV → derives **K_SEAF** from K_AUSF (using SNN so keys are bound to this specific visited network) → hashes XRES* + RAND to create **HXRES*** → packages the **5G SE Authentication Vector** (RAND, AUTN, HXRES*, K_SEAF) → sends it to the visited **AMF**
8. Visited **AMF** forwards RAND + AUTN to your phone as the challenge
9. Your phone's **USIM** verifies **AUTN** (proves the challenge came through a network connected to your home carrier — mutual auth), then computes **RES*** using K + RAND
10. Phone sends **RES*** back to the visited **AMF**
11. Visited **AMF** hashes RES* + RAND → compares against **HXRES*** → match = phone is authentic (visited network's check)
12. Visited **AMF** forwards RES* to the home **AUSF** (through SEPPs)
13. Home **AUSF** compares RES* against **XRES*** → match = authentication confirmed from the home network's perspective (home network's independent check)
14. Home **AUSF** sends **SUPI** + **K_SEAF** to the visited **AMF** (only after both checks pass)
15. Visited **AMF** derives **K_AMF** → **K_gNB** locally from K_SEAF (same as home network from here down)
16. After authentication completes and registration continues, visited **AMF** may assign a **5G-GUTI** for future use _(note: this is part of the registration procedure, not strictly part of 5G-AKA)_
17. You're authenticated, have security keys, and the visited network can now serve you — all without ever knowing K

**Key insight for Security+:** In roaming, the visited network gets enough to authenticate you and derive session keys, but **never touches K or K_AUSF**. This is defense in depth — even if the visited network is compromised, your long-term secret is safe. The home network also independently verifies authentication (a 5G improvement over 4G), preventing a compromised visited network from faking authentication results. This is least-privilege key distribution and Zero Trust principles in action.

---

## **Systematic Mental Model:**

|Abstraction Level|Name|Focus|Security+ Relevance|
|---|---|---|---|
|Level 0|Human View|Phone → Internet → Google → Webpage|3.2-A (Infrastructure scope)|
|Level 1|Major System View|Components + data flow|Multiple (trust boundaries concept)|
|==Level 2==|==Network Architecture==|==gNodeB, RAN, Carrier Core details==|==4.5-A/C (Controls placement)==|
|Level 3|Protocol View|HTTPS → TLS → TCP/IP → Physical|1.4-A/B (Crypto timing)|
|Level 4|Infrastructure View|Actual hardware/components|1.1-G (Physical controls)|
|Level 5|Evidence View|What proves it happened (logs, captures)|4.9-A/B (Data sources)|

---

## **Products:**

- Level 2 carrier architecture diagram (Artifact 3)
	![[Level 2 Diagram.png]]
- Home + roaming 5G-AKA authentication flows (Artifact 4)
    - [[#The Actual 5G-AKA Flow (Simplified)|Home Flow]]
    - [[#The Actual 5G-AKA Flow (Roaming — Simplified)|Roaming Flow]]

---

## **Knowledge Check:**

### Quiz — Segment 1.2 "Understood" Requirements

#### **Question 1 (1.2-E Authentication)**

Your phone just roamed onto a foreign carrier's network. **Explain how the network proves you know secret K without K ever leaving the SIM or the home network — and name the two parties who independently verify your response.**

**Answer:** The network proves you know secret K without it leaving the home network through 2 checks. Visitor network phones back to the home network's AUSF which passes the register request up to UDM/ARPF (that knows the secret K) where the SIDF decrypts the SUCI and sends the challenge packet back to visitor network to send to the UE. The UE validates it's a real network and confirms it knows the secret K as well. The response is sent back to the home network. The home network sends the SUPI and K_SEAF back to the visitor network where the rest of the keys are generated from the visitor network and the UE. In this way, authentication happens without the visitor network knowing the secret K. The two parties are home network UDM and visitor network AMF/SEAF.

**Check:** Correct — with one precision fix on the verifier pair

- The flow you described is right end-to-end: home AUSF → UDM/ARPF (holds K) → SIDF decrypts SUCI → challenge packet → UE validates network + proves K → response home → SUPI + K_SEAF released to visitor network → downstream keys derived locally by visitor AMF and UE. All matches the mapped flow [(ETSI TS 133 501 V17.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/17.13.00_60/ts_133501v171300p.pdf): "The authentication mechanism has in-built home control allowing the home operator to know whether the device is authenticated in a given network and to take final call of authentication."
- **The two independent verifiers are the visited AMF/SEAF and the home AUSF — not the UDM.** The UDM _generates_ XRES* as part of the HE AV, but it doesn't check your answer. The split is: visited AMF hashes your RES* + RAND and compares against HXRES* (local check), then forwards RES* to the home AUSF, which compares it against the real XRES* (home check). UDM hands off verification authority with the AV — the AUSF is the home network's referee, which is exactly what makes the 4G→5G improvement work.

---

#### **Question 2 (1.2-E Authentication — mutual auth)**

When your phone's USIM receives the challenge (RAND + AUTN), **what does it verify before computing its response, and what attack does this defend against?**

**Answer:** The USIM verifies the network is real. This helps defend against a drive by attack.

**Check:** Correct concept, one terminology fix

- Yes — the USIM verifies the network is real (by validating **AUTN**) before computing and sending any response. The network must prove itself first.
- The attack this defends against is a **rogue base station** (fake tower / IMSI catcher), not a "drive-by attack." If a fraudster sets up a fake tower, your phone will reject the challenge because the attacker cannot compute a valid AUTN without knowing K — they'd fail mutual authentication before ever proving anything about _you_. Your instinct named the right threat class (adversary broadcasting as a legitimate network); use the standard term going into the exam.

---

#### **Question 3 (4.1-B Mobile solutions / 4.6-A Provisioning)**

Walk the identity chain end to end: **what is stored permanently on the SIM, what does the phone transmit over the air, what is the network allocate after authentication succeeds, and why does each substitution exist?**

**Answer:** The secret K is stored permanently on the USIM. The phone transmits a registration request containing its SUCI over the air. That request goes to the AMF which asks the AUSF to identify the UE. The AUSF sends that to the UDM/ARPF where the SIDF decrypts the SUCI. This is when the identity is verified. After authentication succeeds a temp ID (5G GUTI) is allocated. The substitutions like SUCI and GUTI exist to help obscure the identity of the UE, but GUTI also helps with efficiency as to not continuously have to do SUCI decrypts.

**Check:** Correct — strongest answer of the three

- K permanently on the USIM ✓, SUCI transmitted over the air ✓, AMF → AUSF → UDM/ARPF/SIDF chain ✓, 5G-GUTI allocated only after successful authentication ✓
- Both substitution rationales are right and well-reasoned: SUCI/GUTI obscure the permanent identity [(NIST CSWP 36C)](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.36C.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to CN." And your efficiency point is a genuine and correct insight — reusing a GUTI skips the full SUCI→SIDF→challenge round-trip, which is exactly why the network prefers the temporary ID once it has one [(ETSI TS 133 501 V16.13.0, Clause 6.1.3.2)](https://www.etsi.org/deliver/etsi_ts/133500_133599/133501/16.13.00_60/ts_133501v161300p.pdf): "the UE should send the SEAF a temporary identifier (a 5G-GUTI) or an encrypted permanent identifier (a SUCI) if a 5G-GUTI has not been allocated."

---

## **Security+ Prelab Snapshot**

|Requirement|Status|Why|Evidence|
|---|---|---|---|
|**1.2-E** Authentication|🟡 **Understood**|✅ Quiz passed (verifier pair corrected)|Home + roaming flow maps, Artifact 3 diagram, quiz answers|
|**1.2-D** Non-repudiation|🔵 Encountered|Home AUSF independent confirmation prevents visited network faking results|Roaming corrections table|
|**1.2-H** Zero Trust|🔵 Encountered|Least-privilege key distribution — visited network never sees K or K_AUSF|"Gets vs. Never Sees" reference table|
|**1.4-B** Encryption|🔵 Encountered|Symmetric (challenge-response) vs. asymmetric (SUCI concealment) distinction established|1a corrections table|
|**2.2-H** Attack surfaces|🔵 Encountered|Air interface + rogue base station threat identified|Quiz Q2 + TB#1 diagram marker|
|**4.1-B** Mobile solutions|🟡 **Understood**|✅ Quiz passed (identity chain + USIM role)|Quiz Q3|
|**4.6-A** Provisioning|🟡 **Understood**|✅ Quiz passed (identity allocation sequence)|Quiz Q3, roaming flow steps 14–16|

---

## Curiosity Questions: 

- **Question 1:** The home network sends the roaming network the SUPI and K_SEAF. That tells the roaming network who you are but the roaming network never learns your secret K. Is it ok that the network knows who you are?
	- **Answer 1:** 

| **Concern**             | **Current Status**                                               |
| ----------------------- | ---------------------------------------------------------------- |
| Post-auth tracking      | Visitor network can correlate sessions via SUPI                  |
| Data retention          | Varies by carrier/regulation; no global standard                 |
| Cross-carrier profiling | Limited technical barriers once SUPI is known                    |
| SUPI length leakage     | Variable-length SUs can reveal info (being addressed in Rel-18+) |
- **Question 2:** How would a carrier track you across into another carrier's network? 
	- **Answer 2:** Cross-Carrier Tracking Threat Model

|#|Threat Vector|Mechanism|Specified Protection|Remaining Gap|Source|Accuracy Rating|
|---|---|---|---|---|---|---|
|1|**Single VPLMN session tracking**|VPLMN receives SUPI + logs activity during visit|None — this is intentional for billing/fraud|No technical restriction on VPLMN retention|TS 33.501 §6.1.3.2; ENISA|**Verified** — explicit in spec architecture|
|2|**Cross-carrier correlation (VPLMN A → B)**|Same SUPI appears in multiple visited networks|Commercial contracts; GDPR jurisdiction|**No technical barrier**; depends on data-sharing agreements|p1sec.com; NIST CSWP 36A|**Analyzed** — inferred from architecture, not explicitly prohibited|
|3|**IPX intermediary aggregation**|IPX providers process roaming signaling for 500+ networks|TLS 1.3 + PRINS on N32-f (between SEPPs)|IPX nodes see decrypted routing data per operational model|Comfone press release (Oct 2025); GSMA NG.113|**Attributed** — vendor marketing claims; no independent verification|
|4|**Home network complete travel history**|HPLMN receives usage/billing records from each VPLMN|Subscriber contract terms|**Intentional design** — enables roaming settlement|Standard roaming architecture|**Verified** — operational requirement per GSMA|
|5|**GUTI refresh inconsistency**|Periodic GUTI updates governed by "should" not "shall"|Mandatory at initial reg, mobility update, paging-response|Operator discretion on periodic renewal timing|TS 33.501 §6.12.3; ShareTechnote analysis|**Verified** — spec language distinguishes "shall" vs "should"|
|6|**Variable-length SUPI leakage**|NAI-format SUPI length observable over radio|Rel-18 studies 10 mitigation options|**Incomplete** in Rel-15/16 deployed networks|Ericsson blog (Apr 2024); 3GPP SA3 study|**Attributed** — research status as of Rel-18, not in all deployments|
|7|**SUCI implementation downgrade**|Networks may accept cleartext SUPI if home doesn't support encryption|ECIES required when both parties support|Silent downgrade possible (implementation-dependent)|NIST CSWP 36A; arXiv:2409.17700v1|**Analyzed** — vulnerability demonstrated; severity debated|
|8|**Lawful intercept access**|State actors with carrier cooperation|Judicial oversight varies by jurisdiction|**Intentional capability** — regulatory requirement|ENISA 5G report (Section 5)|**Verified** — acknowledged in EU assessment|
|9|**Passive radio surveillance (IMSI catcher)**|Attacker broadcasts to force identity disclosure|SUCI ECIES encryption on NG-RAN|Active probing attacks still possible|TS 33.501 §5.2.5; 3GPP Key Issue #3.2|**Verified** — 3GPP concluded low probability but non-zero|
|10|**N32 interconnect compromise**|Unauthorized interception of SEPP-to-SEPP traffic|TLS 1.3 mutual auth + PRINS integrity|Legitimate endpoints still process plaintext internally|TS 33.501 §13; TS 29.573|**Verified** — protects transit, not endpoint handling|

Actor Capability Assessment

|Actor|Data Access|Constraint|Source|
|---|---|---|---|
|Passive radio attacker (no infrastructure access)|❌ Blocked|SUCI ECIES on NG-RAN|TS 33.501 §5.2.5, §6.12.2|
|Visited network operator (active subscriber)|✅ Full (during visit)|None — operational necessity|TS 33.501 §6.1.3.2|
|Home network operator|✅ Full (all historical visits)|None — billing/settlement requirement|GSMA roaming standards|
|IPX provider (intermediary)|⚠️ Partial-to-full|Contractual agreements; GSMA frameworks|GSMA NG.113; vendor documentation|
|State actor with carrier cooperation|✅ Full|Jurisdictional legal process|ENISA report Section 5|
|Non-partner carrier (no roaming agreement)|❌ None|No technical/data-sharing pathway|Roaming architecture design|
- **Question 3:** It seems nothing more can be done but using airplane mode when idle and asking for a SUCI enabled SIM from the carrier. Even so, much of the privacy coverage we're talking about is for 5G. What is the vulnerability if my phone switches between 5G and 4G when traveling? 
	- **Answer 3:**  Core Vulnerability: The Downgrade Attack:

| Aspect                   | 5G SA (Standalone)                                          | 5G NSA (Non-Standalone)                      | 4G LTE                                                   |
| ------------------------ | ----------------------------------------------------------- | -------------------------------------------- | -------------------------------------------------------- |
| **SUCI Support**         | ✅ Required (if home network public key provisioned)         | ⚠️ Optional (often disabled; core is 4G EPC) | ❌ No — IMSI sent in cleartext                            |
| **Base Station Auth**    | ✅ Mutual authentication (UE authenticates network via AUTN) | ⚠️ Partial (relies on 4G EPC)                | ❌ No network authentication (IMSI catcher vulnerability) |
| **Downgrade Resistance** | ✅ Only if 5G-only mode enforced                             | ❌ Falls back to 4G by design                 | N/A                                                      |
| **IMSI Exposure**        | ❌ Protected (SUCI)                                          | ⚠️ Possible via forced LTE fallback          | ✅ Cleartext on initial attach                            |

	- Updated Cross-Carrier Tracking Threat (Including 4G):

|#|Threat|5G SA|5G NSA|4G|Source|
|---|---|---|---|---|---|
|1|SUCI protection|✅ Yes|⚠️ Optional|❌ No (IMSI cleartext)|TS 33.501 §6.12.2; arXiv:1811.02293v1|
|2|Downgrade attack surface|⚠️ If roaming to 4G areas|❌ High (built-in fallback)|N/A|Montsecure Bidding-Down|
|3|Base station authentication|✅ Yes (AUTN validation)|⚠️ Partial|❌ No|TS 33.501 §6.1.3|
|4|Encryption strength|256-bit (NEA2/NEA3)|Mixed (depends on core)|128-bit (EEA2) or broken (A5/1)|TS 33.501 §6.3|
|5|IMSI exposure risk|Low (initial attach)|Medium (NSA fallback)|High (always cleartext on attach)|Mobile Security Authority|
|6|Replay attack resistance|✅ With fresh counters|⚠️ Varies|❌ Weak (TMSI reuse)|p1sec.com 5G-AKA Linkability|
|7|Null-ciphering (EA0/EA0)|⚠️ Allowed by spec|⚠️ Common|⚠️ Allowed|arXiv:2511.03312v1|

	- Bottom Line on 4G/5G Switching:

**The downgrade attack is the weakest link in 5G privacy.** Here's why:

1. **SUCI only works on 5G NR** — Drop to LTE, and you're sending IMSI in cleartext again
2. **Downgrade is standards-compliant** — Attackers exploit normal protocol behavior, not bugs
3. **User has no control** — Phones auto-fallback to 4G for coverage/voice
4. **NSA deployments dominate** — Most "5G" today is actually 4G core with 5G radio
5. **2G fallback still exists** — Some operators permit 2G for voice; A5/1 encryption is trivially broken

**The net effect**: If you're in a 4G-covered area, or if an attacker jams your 5G signal, your phone drops to 4G and the SUCI protection disappears entirely. The same attacker can now harvest your IMSI and track you.

	- References for This Section:

|Source|Relevance|
|---|---|
|arXiv:1811.02293v1 "Defeating the Downgrade Attack on Identity Privacy in 5G"|Core academic analysis of SUCI bypass via LTE|
|3GPP TS 33.501 Annex C|Acknowledges residual NSA deployment risks|
|Mobile Security Authority "Cellular Vulnerabilities"|Practical assessment of IMSI catcher threats in 5G|
|Montsecure "Bidding-Down Attacks and Mitigations in 5G and 4G"|Downgrade attack methodology|
|p1sec.com "5G-AKA Linkability Attacks"|Post-downgrade exploitation scenarios|
|arXiv:2511.03312v1 "Null-ciphering" attack analysis|256-bit encryption weaknesses in 5G|
|SoK WiSec Paper "Legacy and Emerging Attacks"|SUCI optional status critique (Takeaway 6)|
