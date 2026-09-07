# **Driving Question:** "How does the phone authenticate on the carrier network?"

## **PLAN 1a — Home Network Authentication**

### **My Initial Mental Model:**

- This happens when the phone first turns on/mobile data is turned on. The phone connection travels through the tower RAN to the carrier network. 
- The phone sends the carrier the private and public key, the carrier identifies it through the public key. 
- The carrier authenticates the connection and gives it a temporary identity with the network. 
- The carrier forwards the connection through the trust boundary to the public network/internet where it continues its journey. 

#### **Initial Model Accuracies**

| My Guess                                               | Real Engineering Parallel                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Happens when phone turns on / mobile data enabled      | This triggers the **Registration Request** — the UE (User Equipment, your phone) asks to join the network [(3GPP AKMA)](https://www.3gpp.org/technologies/akma): "When a UE registers with the PLMN for the first time, the network performs a primary authentication of the UE."                                                                                                                                                                                                                                                                 |
| Connection travels through tower/RAN to carrier        | The **gNodeB** (the 5G cell tower) is a relay — it forwards signaling (**NAS** messages) from the UE to the AMF (Access and Mobility Management Function) in the core, but doesn't make authentication decisions [(Cisco 5G AMF)](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "N2 - Reference point between R(AN) and AMF."                                                                                           |
| Carrier identifies the phone                           | The phone sends its identity to the network — either as **SUCI** (Subscription Concealed Identifier, the encrypted SUPI) or **5G-GUTI** (temporary identity) if previously allocated [(Telcoma Global)](https://www.telcomaglobal.com/p/5g-identifiers): "5G Subscription Permanent Identifier is a globally unique identifier that is assigned to each subscriber in the 5G system, which is provisioned in the UDM/UDR" — but the _mechanism_ is different from what you described (see corrections).                                           |
| Carrier gives it a temporary identity                  | After successful authentication, the AMF allocates a **5G-GUTI** (Globally Unique Temporary Identity) so the phone doesn't have to send its permanent identity again [(CableLabs)](https://www.cablelabs.com/tech-vision/tech-policy/informed-insights-whitepapers/a-comparative-introduction-to-4g-and-5g-authentication): "the UE should send the SEAF a temporary identifier (a 5G-GUTI) or an encrypted permanent identifier (a SUCI) if a 5G-GUTI has not been allocated."                                                                   |
| Eventually forwards through trust boundary to internet | Correct in the big picture, though this is a _separate_ step from authentication. Authentication establishes identity and keys; establishing a data session (**PDU session**) that actually carries traffic to the Internet is a subsequent process [(3GLTEInfo)](https://www.3glteinfo.com/messages/5g/nas/pdu-session-establishment-request): "Typical state: UE is already registered and is asking the core network to create a new session" — Preconditions section shows PDU session requires prior registration/authentication completion. |

##### **Acronym Glossary — Initial Model Accuracies Table**

- **UE (User Equipment)** = Your phone or any device that connects to the 5G network

- **3GPP (3rd Generation Partnership Project)** = The organization that writes all the rules and technical standards for cellular networks (2G, 3G, 4G, 5G)

- **PLMN (Public Land Mobile Network)** = The carrier's network itself — basically Verizon, AT&T, T-Mobile's infrastructure

- **NAS (Non-Access Stratum)** = The signaling protocol between your phone and the core network (things like 'register me,' 'authenticate me,' 'start a data session'). It's called 'non-access' because these messages are addressed to the core network functions and are transparently relayed by the radio tower (gNodeB) — the gNodeB forwards them without reading or modifying their contents

- **RAN (Radio Access Network)** = Everything that handles the radio connection: cell towers, antennas, and the equipment that turns your phone's wireless signal into something the core network can understand

- **AMF (Access and Mobility Management Function)** = The network function that handles registration, authentication, and mobility (handoffs when you move). Think of it as the "gatekeeper" that decides if your phone is allowed to connect and keeps track of where you are

- **SUCI (Subscription Concealed Identifier)** = Your encrypted ID. Your phone's permanent identity gets encrypted before it ever goes over the air, so eavesdroppers can't read it

- **SUPI (Subscription Permanent Identifier)** = Your actual permanent subscriber ID (basically the 5G version of an IMSI). It's stored on your SIM and in the carrier's database. In 5G, this is always encrypted as SUCI when sent over the air

- **GUTI (Globally Unique Temporary Identity)** = A temporary ID the network assigns to you after authentication. Instead of sending your real ID every time, you send this temporary ID to protect your privacy

- **SEAF (Security Anchor Function)** = A security component that sits between the radio network and the authentication server. In practice, it's co-located with the AMF, so you usually don't hear about it separately

#### **Corrections to Initial Model**

| My Words                                             | Accurate Framing                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Why It Matters for Sec+                                                                                                                                                          |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Phone sends the carrier the private and public key" | **The SIM never sends its secret key.** The SIM stores a long-term shared secret **K** (symmetric key, not a public/private key pair). K exists in two places: on the SIM and in the carrier's UDM. It is **never transmitted.** [(ShareTechnote)](https://www.sharetechnote.com/html/5G/5G_Security.html): "K: The root key, a long-term shared symmetric key stored in the UDM/ARPF and the UE's USIM."                                                                                                   | This is the difference between symmetric and asymmetric crypto. The authentication uses **challenge-response** with a shared secret, not public key exchange.                    |
| "Carrier identifies it through the public key"       | The phone's permanent identity (**SUPI**) is encrypted using the home network's public key, producing the **SUCI** (concealed identifier). The carrier's UDM decrypts SUCI back to SUPI. But the _authentication itself_ uses K via challenge-response — the public key is for **identity privacy**, not authentication. [(NIST 5G)](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.36C.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to CN." | Two separate crypto operations are happening: **asymmetric encryption** protects identity in transit; **symmetric challenge-response** proves the SIM knows K.                   |
| (Missing)                                            | **Mutual authentication** — the phone authenticates the network too, not just the network authenticating the phone. The network sends **AUTN** (authentication token), and the SIM verifies it. Only then does the SIM respond with **RES** (its response to the challenge). [(free5GC)](https://free5gc.org/blog/20251029/20251029): "USIM validates AUTN using the shared secret K, computes RES… The 5G-AKA procedure ensures mutual authentication of the UE and the serving network."                  | Security+ covers mutual authentication. This is also a trust boundary — the phone needs to verify it's talking to a legitimate network, not a rogue base station (IMSI catcher). |
| (Missing)                                            | **Key derivation hierarchy** — after authentication succeeds, K seeds a tree of derived keys: **K_AUSF → K_SEAF → K_AMF → K_gNB**. Different keys protect different layers (radio link, NAS signaling, user plane). [(3GPP AKMA)](https://www.3gpp.org/technologies/akma): "The AUSF stores the root session key KAUSF and further keys are derived from this key."                                                                                                                                         | Security+ tests understanding of layered key management and why deriving separate keys for separate purposes matters.                                                            |

##### **Acronym Glossary — Corrections Table**

- **K (Long-Term Secret Key)** = A secret number stored on your SIM card AND in the carrier's database. Both sides have the same one, and it's used to prove you're who you say you are. The key itself is **never sent over the air** — instead, both sides do math with it and compare results

- **UDM (Unified Data Management)** = The carrier's database that holds all your subscriber information, including your secret key K. This is where the carrier "knows" who you are

- **USIM (Universal Subscriber Identity Module)** = The actual chip on your SIM card that stores your secret key K. It's the hardware that does the crypto calculations for authentication

- **SUPI (Subscription Permanent Identifier)** = Your permanent subscriber ID (like a username for the carrier). In 5G, this is encrypted before sending over the air to protect privacy

- **SUCI (Subscription Concealed Identifier)** = Your SUPI after it's been encrypted. Think of it as "your real name wrapped in an envelope that only the home carrier can open"

- **AUTN (Authentication Token)** = A code the network sends to your phone to prove _it_ is legitimate. If your phone can't verify the AUTN, it knows it might be talking to a fake tower (rogue base station)

- **RES (Response)** = The number your phone computes using the secret key K and a random challenge from the network. If it matches what the network expected, authentication succeeds

- **5G-AKA (5G Authentication and Key Agreement)** = The actual protocol name for how 5G phones authenticate. "AKA" means both sides prove they know the secret without sending the secret itself

- **K_AUSF (Key for Authentication Server Function)** = The first session key derived after authentication. It's the "root" for all other keys that follow

- **K_SEAF (Key for Security Anchor Function)** = A derived key used to secure communications between the network and your phone at the security anchor level

- **K_AMF (Key for Access and Mobility Management Function)** = A derived key used to protect NAS signaling messages (registration, authentication commands, etc.)

- **K_gNB (Key for Next Generation NodeB)** = A derived key used to encrypt the actual radio link between your phone and the cell tower

- **AUSF (Authentication Server Function)** = The network function that actually runs the authentication procedure. It talks to the UDM to get credentials, sends challenges to the phone, and verifies responses

- **gNB (Next Generation NodeB)** = The 5G version of a cell tower/base station. It handles the radio connection but doesn't make authentication decisions

- **SEAF (Security Anchor Function)** = A security component that acts as the bridge between the radio network and the authentication server. Usually co-located with the AMF

##### **Quick Reference — Why the Key Hierarchy Matters**

| Derived Key | What It Protects                                                                             |
| ----------- | -------------------------------------------------------------------------------------------- |
| K_AUSF      | Root session key — created by the auth server (AUSF); the ancestor of every key that follows |
| K_SEAF      | Bridge key handed to the serving network (held by the SEAF, co-located with the AMF)         |
| K_AMF       | NAS signaling — registration, authentication commands, mobility messages                     |
| K_gNB       | Radio link — encrypts the actual wireless traffic between your phone and the tower           |

##### **The Actual 5G-AKA Flow (Simplified)**

Here's the corrected chronology for what happens during authentication:

1. Phone turns on → wants to join the carrier network 
2. Phone sends a "register me" request to the cell tower (gNB) → forwarded to the gatekeeper (AMF) - Request includes your encrypted ID (SUCI) or temporary ID (GUTI) from last time 
3. Gatekeeper (AMF) asks the auth server (AUSF) to verify you - Includes your encrypted ID and which carrier network you're on (SNN) 
4. Auth server asks the subscriber database (UDM) for your credentials 
5. Database (UDM) decrypts your ID, looks up your secret key K, and generates a challenge package - Random number (RAND), auth token (AUTN), expected answer (XRES) 
6. Challenge sent back to your phone: "Here's a random number and proof we're legitimate" 
7. Your phone's SIM checks the auth token (proves we're a real network), then computes the answer using the secret key K (mutual auth)
8. Phone sends answer (RES) back up the chain to the auth server (AUSF) 
9. Auth server compares your answer (RES) against the expected one (XRES) → match = you're in 
10. Keys are generated for both sides independently from K: **K → CK/IK → K_AUSF → K_SEAF → K_AMF** → final keys for NAS, RRC, and user-plane encryption
11. Gatekeeper gives you a temporary ID (GUTI) for future use 
12. You're authenticated and have security keys

**Key insight for Security+:** The secret K never leaves the SIM or the UDM. Instead, the network sends a random challenge (RAND), and both sides independently compute a response using K. If the responses match, both sides have proven they know K without ever transmitting it. This is classic **challenge-response authentication** — a Security+ staple.

###### **Technical Reference (Full Terminology)**

- **5G-GUTI (5G Globally Unique Temporary Identity)** = Same as GUTI from the earlier glossary, just with "5G-" in front. It's your temporary ID the network assigns after authentication so you don't have to keep sending your real identity

- **SNN (Serving Network Name)** = The name of the carrier network currently trying to authenticate you (e.g., "Verizon" or "T-Mobile"). This matters because the phone's keys are derived partly based on _which_ network is serving you — it prevents keys from one carrier being reused on another

- **ARPF (Authentication Credential Repository and Processing Function)** = The part of the UDM that actually stores the secret key K and runs the crypto math. Think of it as the vault inside the UDM — the UDM is the building, the ARPF is the safe

- **RAND (Random Challenge)** = A random number the network generates and sends to your phone. Your phone uses K to do math with RAND and produce RES. The randomness ensures every authentication is unique and can't be replayed

- **XRES (Expected Response)** = The answer the UDM computes. First the USIM/UDM use K to derive CK and IK, then XRES is derived from those plus RAND. Your phone computes RES the same way. If they match, authentication succeeds. It's what your phone's RES _should_ match if authentication is successful. The "X" prefix stands for "expected" — it's the key the network holds onto until your phone replies

- **Authentication Vector** = A package of values the UDM generates for 5G-AKA: RAND, AUTN, XRES, and K_AUSF (anchor key). The network sends RAND and AUTN to your phone as a challenge, holds XRES to check your answer, and K_AUSF becomes the root for all session keys

---
_The flow above assumes the phone is on its home carrier's network. When roaming, the authentication path changes because the visited network doesn't have the subscriber's secret key K. This leads us to the flow below._

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
|Phone sends registration request; gNodeB transports to AMF with encrypted identity|Same as home network — the **UE** sends a **Registration Request** with **SUCI** (or **5G-GUTI**), the visited **gNodeB** relays it to the visited **AMF** [(3glteinfo)](https://www.3glteinfo.com/call-flows/5g/roaming-authentication): "A roaming UE starts registration or service in a visited network and must be authenticated against home-network credentials."|
|Credentials aren't found locally — need to contact home carrier|The visited network has no subscriber database for you. The visited **AMF** must request authentication support from the home network's **AUSF** [(LTE5G Hub)](https://lte5ghub.com/ausf): "In a roaming case the visited network can no longer authenticate a subscriber on its own; the home network must be involved and must confirm the outcome."|
|Foreign carrier cross-talks with the phone's native carrier|The visited AMF contacts the home **AUSF** through inter-network gateways called **SEPPs** (Security Edge Protection Proxies). The AUSF acts as a proxy to the home **UDM**, which holds your credentials [(3GPP)](https://www.3gpp.org/news-events/3gpp-news/sec-5g): "In the roaming architecture, the home and the visited network are connected through SEcurity Protection Proxy (SEPP) for the control plane of the internetwork interconnect."|
|Identity is decrypted|The **SUCI** is decrypted back to **SUPI** by the home network's **UDM** (specifically a function called **SIDF** — Subscription Identifier De-concealing Function inside the UDM). The visited network never sees the SUPI [(Devopedia)](https://devopedia.org/5g-authentication): "Given SUCI, SIDF will de-conceal it. UDM sends 5G HE AV and SUPI to AUSF in the response."|
|Authentication settled using K; phone affirms it knows K|The challenge-response still uses **K** via **5G-AKA** — the home **UDM** generates **RAND**, **AUTN**, and **XRES** using K, the phone's **USIM** verifies **AUTN** (mutual auth) and computes **RES** [(ShareTechnote)](https://www.sharetechnote.com/html/5G/5G_Security.html): "Both UE and home network share a long-term secret key. Network creates a random number challenge RAND. Using the secret key and RAND, it computes an expected response XRES."|
|Both generate follow-on keys; native carrier no longer needed|After authentication succeeds, the home **AUSF** derives **K_SEAF** from **K_AUSF** and sends it to the visited network. The visited network then derives **K_AMF** and **K_gNB** locally — no further home involvement needed for session keys [(5G/6G Academy)](https://www.5g6gacademy.com/learn/5g-security-architecture): "K_AUSF never leaves the home network. Even in roaming scenarios, the visited AMF only receives K_SEAF."|
|Eventually requests pushed to public routing|After a **PDU session** is established (separate from authentication), traffic flows through the visited network to the Internet — same as home, just routed through visited infrastructure|

##### **Acronym Glossary — Initial Model Accuracies Table**

- **SEPP (Security Edge Protection Proxy)** = A security gateway that sits at the border between two carrier networks. When the visited network and home network need to talk, all their signaling traffic passes through SEPPs on both sides. Think of it as a customs checkpoint for inter-carrier communications — it filters, protects, and authenticates the connection between the two networks
- **SIDF (Subscription Identifier De-concealing Function)** = The specific function inside the home network's UDM that decrypts SUCI back to SUPI. Think of it as the only person with the key to the envelope your phone sends — nobody else in the visited network can open it
- **5G HE Authentication Vector (Home Environment AV)** = The full package the home UDM generates: RAND, AUTN, XRES*, and K_AUSF. This never leaves the home network intact — the AUSF transforms it before sending anything to the visited network
- **5G SE Authentication Vector (Serving Environment AV)** = The trimmed-down package the AUSF sends to the visited network: RAND, AUTN, HXRES*, and K_SEAF. Notice K_AUSF and XRES* are NOT included — the visited network gets hashed versions (HXRES*) instead, so it can verify the phone's response without seeing the original values
- **HXRES* (Hashed Expected Response)** = A hash of XRES* and RAND. The AUSF creates this so the visited network can check whether the phone's response (RES*) is correct, without ever seeing the real XRES*. It's like giving someone the answer key to a hash but not the actual answer
- **NRF (Network Repository Function)** = A directory service inside the 5G core. When the visited AMF needs to find the home AUSF, it (or the AUSF) can query the NRF to look up the right address — like a phone book for network functions

#### **Corrections to Initial Model**

| My Words                                                                | Accurate Framing                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Why It Matters for Sec+                                                                                                                                                                                          |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Phone is handed off to a new carrier by a tower command"               | Inter-carrier handover exists, but the more common roaming scenario is the phone registering fresh on a visited network (turning on abroad, losing home coverage). Either way, the visited network must authenticate you from scratch — a handoff command doesn't transfer trust between carriers [(3glteinfo)](https://www.3glteinfo.com/call-flows/5g/roaming-authentication): "Start state: UE is attached to a visited network but is not yet trusted for secure roaming service."                                                                                                                                         | Trust doesn't transfer between organizations. Each carrier maintains its own trust domain — relevant to Zero Trust (1.2-H) and trust boundary analysis.                                                          |
| "AMF forwards to the necessary server which forwards to database"       | More precisely: visited **AMF** → (through **SEPP**) → home **AUSF** → home **UDM/ARPF**. The AUSF is the authentication proxy; the UDM/ARPF holds K and generates the challenge package [(Mpirical)](https://www.mpirical.com/knowledge-base/5g-security-when-roaming-part-1): "The authentication procedure begins with the AMF in the visited network requesting authentication parameters from the AUSF in the home network. This is passed through the SEPPs on the edge of each of the core networks."                                                                                                                   | Understanding the chain of custody for authentication requests — who sees what, and where the sensitive operations happen — maps to secure access (3.2-D) and infrastructure considerations (3.2-A).             |
| "Cross-talk with the phone's native carrier for credential information" | The visited network **never receives K**. The home UDM generates the **5G HE Authentication Vector** (RAND, AUTN, XRES, K_AUSF) and sends only the **5G SE Authentication Vector** (RAND, AUTN, HXRES*, K_SEAF) to the visited network. K stays in the home network [(Devopedia)](https://devopedia.org/5g-authentication): "5G HE Authentication Vector: Consists of RAND, AUTN, XRES*, and K_AUSF. AUSF obtains this from UDM/ARPF." [(5G/6G Academy)](https://www.5g6gacademy.com/learn/5g-security-architecture): "K_AUSF never leaves the home network. Even in roaming scenarios, the visited AMF only receives K_SEAF." | This is layered key management and least-privilege design — the visited network gets exactly what it needs to serve you, and nothing more. Maps to cryptographic solutions (1.4-A/B) and access control (2.5-B). |
| "Or either let the native tower handle the credential confirmation"     | The home network doesn't delegate authentication to a "native tower." Instead, the home **AUSF** verifies the UE's response (**RES** vs **XRES***) independently. This is a 5G improvement over 4G — the home network gets final confirmation that authentication succeeded [(Award Solutions)](https://www.awardsolutions.com/portal/resources/5g-security-improvements): "5G takes security one step further in the authentication procedure when the home network receives the UE response from the visited network to authenticate independently of the visited network's authentication."                                 | Home-network confirmation prevents a compromised visited network from falsely claiming you authenticated. Relevant to non-repudiation (1.2-D) and Zero Trust (1.2-H).                                            |
| "Phone generates its package that affirms it knows K"                   | The phone doesn't initiate — it **responds to a challenge**. The flow is: network sends RAND + AUTN → phone verifies AUTN (proves network legitimacy) → phone computes RES using K + RAND → phone sends RES back [(ShareTechnote)](https://www.sharetechnote.com/html/5G/5G_Security.html): "UE verifies that AUTN is valid. It then computes RES* and sends this back to the home network."                                                                                                                                                                                                                                   | Same challenge-response principle as home auth, but the chain of relay is longer. The phone can't tell (and shouldn't care) whether it's roaming — the SIM just does crypto with what it receives.               |

##### **Acronym Glossary — Corrections Table**

- **K_AUSF** = The root session key derived during authentication. Critically: **this key never leaves the home network**, even in roaming. The visited network never sees it [(5G/6G Academy)](https://www.5g6gacademy.com/learn/5g-security-architecture): "K_AUSF never leaves the home network. Even in roaming scenarios, the visited AMF only receives K_SEAF."
- **K_SEAF** = The key the AUSF derives from K_AUSF and hands to the visited network. This is the highest key the visited network ever gets — everything downstream (K_AMF, K_gNB) is derived from it locally
- **SNN (Serving Network Name)** = The name of the visited network requesting authentication. This is baked into the key derivation formula, which means keys generated for one visited network won't work on a different one. This prevents a compromised visited network from using your keys elsewhere [(Mpirical)](https://www.mpirical.com/knowledge-base/5g-security-when-roaming-part-1): "This ensures that for authentication to be successful, the visited network requesting authentication vectors from the home network must be the same network that the device is actually connected to during the authentication procedure."
- **Home Network Confirmation** = A 5G-specific improvement where the home AUSF independently verifies the UE's response (RES* vs XRES*) rather than trusting the visited network's verdict. In 4G, the visited network did all verification — 5G adds home-network oversight [(Award Solutions)](https://www.awardsolutions.com/portal/resources/5g-security-improvements): "5G takes security one step further in the authentication procedure when the home network receives the UE response from the visited network to authenticate independently of the visited network's authentication."

##### **Quick Reference — What the Visited Network Gets vs. Doesn't Get**

|The Visited Network Receives|The Visited Network Never Sees|
|---|---|
|RAND + AUTN (to challenge the phone)|K (the long-term secret key)|
|HXRES* (hashed expected response, to verify the phone's answer)|XRES* (the real expected response)|
|K_SEAF (to derive local session keys)|K_AUSF (the root session key)|
|SUPI (only after authentication succeeds)|The private key used to decrypt SUCI|

##### **The Actual 5G-AKA Flow (Roaming — Simplified)**

1. Phone arrives on visited network → sends **Registration Request** with **SUCI** (or **5G-GUTI** if previously assigned) to the visited **gNodeB**
2. Visited **gNodeB** forwards the request to the visited **AMF** (just like home — the tower is still just a relay)
3. Visited **AMF** sees it doesn't have credentials for this subscriber → sends an authentication request to the home **AUSF** (through **SEPPs** on both sides)
4. Home **AUSF** receives the request (includes your SUCI and the **SNN** — Serving Network Name of the visited carrier)
5. Home **AUSF** forwards the request to the home **UDM/ARPF**
6. Home **UDM** decrypts **SUCI** → recovers **SUPI** → looks up your secret key **K** → generates the **5G HE Authentication Vector**: RAND, AUTN, XRES*, K_AUSF
7. Home **AUSF** receives the HE AV → derives **K_SEAF** from K_AUSF (using SNN so keys are bound to this specific visited network) → hashes XRES* + RAND to create **HXRES*** → packages the **5G SE Authentication Vector** (RAND, AUTN, HXRES*, K_SEAF) → sends it to the visited **AMF**
8. Visited **AMF** forwards RAND + AUTN to your phone as the challenge
9. Your phone's **USIM** verifies **AUTN** (proves the challenge came through a network connected to your home carrier — mutual auth), then computes **RES*** using K + RAND
10. Phone sends **RES*** back to the visited **AMF**
11. Visited **AMF** hashes RES* + RAND → compares against **HXRES*** → match = phone is authentic (visited network's check)
12. Visited **AMF** forwards RES* to the home **AUSF** (through SEPPs)
13. Home **AUSF** compares RES* against **XRES*** → match = authentication confirmed from the home network's perspective (home network's independent check)
14. Home **AUSF** sends **SUPI** + **K_SEAF** to the visited **AMF** (only after both checks pass)
15. Visited **AMF** derives **K_AMF** → **K_gNB** locally from K_SEAF (same as home network from here down)
16. Visited **AMF** assigns a **5G-GUTI** for future use
17. You're authenticated, have security keys, and the visited network can now serve you — all without ever knowing K

**Key insight for Security+:** In roaming, the visited network gets enough to authenticate you and derive session keys, but **never touches K or K_AUSF**. This is defense in depth — even if the visited network is compromised, your long-term secret is safe. The home network also independently verifies authentication (a 5G improvement over 4G), preventing a compromised visited network from faking authentication results. This is least-privilege key distribution and Zero Trust principles in action.
## **Systematic Mental Model:**

[[Mission 01 Passport]] Section 6 (System Architecture)

| Abstraction Level | Name                     | Focus                                    | Security+ Relevance                 |
| ----------------- | ------------------------ | ---------------------------------------- | ----------------------------------- |
| Level 0           | Human View               | Phone → Internet → Google → Webpage      | 3.2-A (Infrastructure scope)        |
| Level 1           | Major System View        | Components + data flow                   | Multiple (trust boundaries concept) |
| ==Level 2==       | ==Network Architecture== | ==gNodeB, RAN, Carrier Core details==    | ==4.5-A/C (Controls placement)==    |
| Level 3           | Protocol View            | HTTPS → TLS → TCP/IP → Physical          | 1.4-A/B (Crypto timing)             |
| Level 4           | Infrastructure View      | Actual hardware/components               | 1.1-G (Physical controls)           |
| Level 5           | Evidence View            | What proves it happened (logs, captures) | 4.9-A/B (Data sources)              |

## **Products:**

- Level 2 carrier architecture diagram (Artifact 3)
![[Level 2 Diagram.png]]
- Home + roaming 5G-AKA authentication flows (Artifact 4)  
	- [[#The Actual 5G-AKA Flow (Simplified)| Home Flow]] 
	- [[#The Actual 5G-AKA Flow (Roaming — Simplified)|Roaming Flow]]

## **Knowledge Check:**

### Quiz — Segment 1.2 "Understood" Requirements

#### **Question 1 (1.2-E Authentication)**

Your phone just roamed onto a foreign carrier's network. **Explain how the network proves you know secret K without K ever leaving the SIM or the home network — and name the two parties who independently verify your response.**

**Answer:** The network proves you know secret K without it leaving the home network through 2 checks. Visitor network phones back to the home network's AUSF which passes the register request up to UDM/ARPF (that knows the secret K) where the SIDF decrypts the SUCI and sends the challenge packet back to visitor network to send to the UE. The UE validates it's a real network and confirms it knows the secret K as well. The response is sent back to the home network. The home network sends the SUPI and K_SEAF back to the visitor network where the rest of the keys are generated from the visitor network and the UE. In this way, authentication happens without the visitor network knowing the secret K. The two parties are home network UDM and visitor network AMF/SEAF.

**Check:** Correct — with one precision fix on the verifier pair

- The flow you described is right end-to-end: home AUSF → UDM/ARPF (holds K) → SIDF decrypts SUCI → challenge packet → UE validates network + proves K → response home → SUPI + K_SEAF released to visitor network → downstream keys derived locally by visitor AMF and UE. All matches the mapped flow [(3GPP)](https://www.3gpp.org/news-events/3gpp-news/sec-5g): "The authentication mechanism has in-built home control allowing the home operator to know whether the device is authenticated in a given network and to take final call of authentication."
- **The two independent verifiers are the visited AMF/SEAF and the home AUSF — not the UDM.** The UDM _generates_ XRES* as part of the HE AV, but it doesn't check your answer. The split is: visited AMF hashes your RES* + RAND and compares against HXRES* (local check), then forwards RES* to the home AUSF, which compares it against the real XRES* (home check). UDM hands off verification authority with the AV — the AUSF is the home network's referee, which is exactly what makes the 4G→5G improvement work.

---

#### **Question 2 (1.2-E Authentication — mutual auth)**

When your phone's USIM receives the challenge (RAND + AUTN), **what does it verify before computing its response, and what attack does this defend against?**

**Answer:** The USIM verifies the network is real. This helps defend against a drive by attack.

**Check:** Correct concept, one terminology fix

- Yes — the USIM verifies the network is real (by validating **AUTN**) before computing and sending any response. The network must prove itself first.
- The attack this defends against is a **rogue base station** (fake tower / IMSI catcher), not a "drive-by attack." If a fraudster sets up a fake tower, your phone will reject the challenge because the attacker cannot compute a valid AUTN without knowing K — they'd fail mutual authentication before ever proving anything about _you_. Your instinct named the right threat class (adversary broadcasting as a legitimate network); use the standard term going into the exam.

---

#### **Question 3 (4.1-B Mobile solutions / 4.6-A Provisioning)**

Walk the identity chain end to end: **what is stored permanently on the SIM, what does the phone transmit over the air, what is the network allocate after authentication succeeds, and why does each substitution exist?**

**Answer:** The secret K is stored permanently on the USIM. The phone transmits a registration request containing its SUCI over the air. That request goes to the AMF which asks the AUSF to identify the UE. The AUSF sends that to the UDM/ARPF where the SIDF decrypts the SUCI. This is when the identity is verified. After authentication succeeds a temp ID (5G GUTI) is allocated. The substitutions like SUCI and GUTI exist to help obscure the identity of the UE, but GUTI also helps with efficiency as to not continuously have to do SUCI decrypts

**Check:** Correct — strongest answer of the three

- K permanently on the USIM ✓, SUCI transmitted over the air ✓, AMF → AUSF → UDM/ARPF/SIDF chain ✓, 5G-GUTI allocated only after successful authentication ✓
- Both substitution rationales are right and well-reasoned: SUCI/GUTI obscure the permanent identity [(NIST 5Q)](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.36C.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to CN." And your efficiency point is a genuine and correct insight — reusing a GUTI skips the full SUCI→SIDF→challenge round-trip, which is exactly why the network prefers the temporary ID once it has one [(CableLabs)](https://www.cablelabs.com/tech-vision/tech-policy/informed-insights-whitepapers/a-comparative-introduction-to-4g-and-5g-authentication): "the UE should send the SEAF a temporary identifier (a 5G-GUTI) or an encrypted drawing (a SUCI) if a 5G-GUTI has not been allocated."

---

## **Security+ Prelab Snapshot**

[[Sub-requirements Matrix]]

|Requirement|Status|Why|Evidence|
|---|---|---|---|
|**1.2-E** Authentication|🟡 **Understood**|✅ Quiz passed (verifier pair corrected)|Home + roaming flow maps, Artifact 3 diagram, quiz answers|
|**1.2-D** Non-repudiation|🔵 Encountered|Home AUSF independent confirmation prevents visited network faking results|Roaming corrections table|
|**1.2-H** Zero Trust|🔵 Encountered|Least-privilege key distribution — visited network never sees K or K_AUSF|"Gets vs. Never Sees" reference table|
|**1.4-B** Encryption|🔵 Encountered|Symmetric (challenge-response) vs. asymmetric (SUCI concealment) distinction established|1a corrections table|
|**2.2-H** Attack surfaces|🔵 Encountered|Air interface + rogue base station threat identified|Quiz Q2 + TB#1 diagram marker|
|**4.1-B** Mobile solutions|🟡 **Understood**|✅ Quiz passed (identity chain + USIM role)|Quiz Q3|
|**4.6-A** Provisioning|🟡 **Understood**|✅ Quiz passed (identity allocation sequence)|Quiz Q3, roaming flow steps 14–16|
