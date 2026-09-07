# **Driving Question:** "When I press Enter on `google.com`, what is the very first thing my phone has to know or do before it can send the request toward Google?"

## My Initial Mental Model: 

- Phone wakes up, authenticates with service provider under the coverage of whatever tower you're closest to
- When you drive, it's pinging the tower here and there - just a "where are you?" or also background processes
- When you open the browser, the browser probably preloads pages, bookmarks, etc and starts talking to the nearest tower
- Phone establishes a handshake with nearest tower, type google.com, hits tower, tower routes it to nearest server through backhaul, nearest server might have a cache but may not be google server but can answer request. 
- Request starts making it's way back to your phone

### **Initial Model Accuracies** 

| My Guess                                           | Real Engineering Parallel                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Phone authenticates with carrier before using data | Pre-shared credentials (SIM) enable authentication ([NIST 5G](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.36C.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to CN.")                                                                                                                                                       |
| Driving past towers = periodic "where are you?"    | This is called **mobility/handover** — tower changes without dropping session ([telecomHall 5G Handover](https://www.telecomhall.net/t/how-does-handover-work-in-lte-and-5g/36588): "Handover is the process of transferring an active call or data session from one cell tower to another without dropping the connection as a user moves.")                                               |
| Browser preloads/background processes              | Pre-fetching, caching, keep-alive connections ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Caching): "The HTTP cache stores a response associated with a request and reuses the stored response for subsequent requests.")                                                                                                                                      |
| Tower as entry point to network                    | Radio Access Network (RAN) is the gateway ([Cisco 5G AMF](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "N2 - Reference point between R(AN) and AMF.")                                                                                                            |
| Backhaul carries traffic to carrier core           | Fiber/microwave links from tower to core ([Cisco 5G xHaul](https://www.cisco.com/site/us/en/solutions/service-provider/5g-network-architecture/5g-transport/converged-5g-xhaul-transport/index.html): "Operators have simplified the number of network layers down to a Dense-Wave Division Multiplexing (DWDM) / fiber foundation overlaid by a packet routing/switching infrastructure.") |
| Edge/cache servers might answer                    | CDNs like Google's edge reduce round-trips ([Cloudflare CDN](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/): "A CDN is a geographically distributed group of servers that caches content close to end users.")                                                                                                                                                                     |
| Response travels back along the path               | Return path follows routing tables ([Cisco Routing](https://www.cisco.com/site/us/en/learn/topics/networking/what-is-routing.html): "The routing process starts when software on a host device uses a packet's contents, destination, or purpose to select a possible route from a routing table.")                                                                                         |

### **Corrections to Initial Model** 

| My Words                                 | Accurate Framing                                                                        | Why It Matters for Sec+                                                                                                                                                                                                                                                                                          |
| ---------------------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Phone establishes handshake with tower" | **Tower is transparent** — phone authenticates with **carrier core**, tower just relays | Authentication happens at the **core** (5GC), not at the radio tower (gNodeB). This is a trust boundary.                                                                                                                                                                                                         |
| "Tower routes it to nearest server"      | **Carrier core + Internet routers** do the routing, not the tower                       | Towers don't make routing decisions. The **Internet** layer handles this. ([Cisco 5G AMF](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "N2 - Reference point between R(AN) and AMF.") |
| "Type google.com, hits tower"            | **DNS lookup happens FIRST** — before "hits tower"                                      | Browser needs an IP address before it can send packets. DNS is a distinct step. ([Cloudflare DNS](...): "Once the 8 steps of the DNS lookup have returned the IP address... the browser is able to make the request")                                                                                            |
| "Nearest server might have cache"        | **Google edge servers** serve cached content; they ARE Google infrastructure            | CDN nodes are still Google-managed. Not a third-party proxy. ([Google Cloud CDN](https://cloud.google.com/cdn): "Cloud CDN uses Google's global edge network to serve content closer to your users. Originally built to serve Google's core applications like Google Search, Gmail, and Maps.")                  |
	- **Note: Why DNS matters for Security+:**
		- If DNS is manipulated → you get sent to fake site (phishing)
		- DNS queries are visible to carrier (privacy concern)
		- DNSSEC/encrypted DNS protect against manipulation
	
#### **Revised/Correct Chronology**
- _Pre-condition: Phone is already authenticated to 5G Core and has an active data session with an assigned IP address (covered in phases 1.2 and 1.3)_
- Press Enter on google.com
- Browser checks cache for IP
- If no cache → DNS query sent
- DNS resolver returns IP address(es)
- Initiate TCP/QUIC connection to that IP
- TLS handshake (encryption + certificate validation) ([RFC 8446 TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446.html): "The TLS protocol provides communications security over the Internet. The protocol allows client/server applications to communicate in a way that is designed to prevent eavesdropping, tampering, or message forgery.")
- HTTP GET request
- Google edge/server responds
- Response returns along reverse path
## A Systematic Mental Model:

[[Mission 01 Passport]] Section 6 (System Architecture)

| Abstraction Level | Name                 | Focus                                    | Security+ Relevance                 |
| ----------------- | -------------------- | ---------------------------------------- | ----------------------------------- |
| ==Level 0==           | ==Human View==           | ==Phone → Internet → Google → Webpage==      | ==3.2-A (Infrastructure scope)==        |
| ==Level 1==           | ==Major System View==    | ==Components + data flow==                   | ==Multiple (trust boundaries concept)== |
| Level 2           | Network Architecture | gNodeB, RAN, Carrier Core details        | 4.5-A/C (Controls placement)        |
| Level 3           | Protocol View        | HTTPS → TLS → TCP/IP → Physical          | 1.4-A/B (Crypto timing)             |
| Level 4           | Infrastructure View  | Actual hardware/components               | 1.1-G (Physical controls)           |
| Level 5           | Evidence View        | What proves it happened (logs, captures) | 4.9-A/B (Data sources)              |

Lessons Learned: Never skip the high (low level) abstraction view that helps establish the journey. This helps avoid going in depth on the wrong problem set/journey and keeps the focus clean. 
### **Human View using Level 0 Diagram** 

- **My initial Level 0 Diagram:** Phone to tower to internet to server 

- **Correct Level 0 Diagram:**
		![[Level 0 Diagram.png]]
	- Note: Tower and server would be data flow rather than what humans see. This is a very high level diagram. 

### **Major System View using Level 1 Diagram:** 

- **My initial Level 1 Diagram:** Phone to tower to backhaul/fiber to a non-Google server carrying a cache from Google servers for basic requests

- **Correct Level 1 Diagram:**
		![[Level 1 Diagram.png]]
## **Products:** 
- Level 0 and Level 1 diagrams
## **Knowledge Check:** 
### Quiz — Segment 1.1 "Understood" Requirements

#### **Question 1 (1.2-E Authentication)**

Looking at the Level 1 diagram's 5G Core box, it says "Authentication (SIM)". Based on what we discussed and your initial mental model:

**Where does the phone actually authenticate — at the tower, or somewhere else? And what credential does it use?**

**Answer:** The phone authenticates at the 5G Core rather than the tower. The credential is SIM. Every SIM has an identity burned in.

**Check:** Correct

- Tower (gNodeB) is just a relay — it doesn't validate credentials ([Cisco 5G AMF](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "The REST EP sends an Authentication Information Request to the AUSF and gets a response. The response from the AUSF is forwarded to the AMF service.")
- SIM contains permanent identity (**SUPI** in 5G, hidden during transmission as **SUCI**) ([NIST 5G](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.36C.pdf): "SUPI is encrypted into a Subscription Concealed Identifier (SUCI) while it is signaled from the UE to CN.")
- Authentication happens at the **AUSF/UDM** functions inside 5GC ([Cisco 5G AMF](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "N8 - Reference point between AMF and UDM. N12 - Reference point between AUSF and AMF.")
- **Minor precision:** Not just "identity burned in" — the SIM stores a long-term secret key (**K**) that's never transmitted. The network challenges the SIM to prove it knows K without revealing K itself (mutual authentication) *(Reference 3GPP 5G-AKA specification)*

---

#### **Question 2 (1.2-F Authorization)**

After authentication succeeds, the phone gets network access. But **how does the carrier decide what the phone is _allowed_ to do? What's being checked beyond "are you who you say you are"?**

**Answer:** The carrier decides using policy. What you're allowed to do and what you should have access to would be questions after validating identity.

**Check:** Correct

- After authentication, the **Policy Control Function (PCF)** decides what the phone can access ([Cisco 5G AMF](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "N15 - Reference point between AMF and PCF.")
- Checks: data plan, roaming status, subscribed services, time-of-day restrictions
- **Session Management Function (SMF)** enforces the policies on the UPF ([Cisco 5G AMF](https://www.cisco.com/c/en/us/td/docs/wireless/ucc/amf/2026-01/config-and-admin/ucc-5g-amf-configuration-and-administration-guide-release-2026-01/m_amf-overview.html): "N11 - Reference point between AMF and SMF... If there is any vestigial PDU state for the UE in the SMF, the AMF clears the state.")
- **Minor addition:** Authorization is separate from authentication. You could be authenticated but still blocked from certain services (parental controls, paywalled content, bandwidth limits).

---

#### **Question 3 (3.2-A Infrastructure Considerations)**

Looking at your Level 1 diagram, you have five major segments (User Device → Radio → Carrier → Internet → Google). **Pick one segment and explain what makes it different from the others in terms of security considerations.**

**Answer:** Internet would be different from the others, because it begins public routing and other device connections. This makes it more dangerous in a way from sheer exposure.

**Check:** Correct

- Only segment you **don't control** at all
- Any organization can peer or transit through it
- **Trust Boundary #2** is the last point where the carrier enforces security before traffic becomes "someone else's problem" ([OWASP Web Security](https://cheatsheetseries.owasp.org/cheatsheets/Web_Service_Security_Cheat_Sheet.html): "Transport confidentiality protects against eavesdropping and man-in-the-middle attacks against web service communications to/from the server.")
- **Additional context:** The carrier can inspect/filter traffic before it exits (firewall/DPI). Once on the public Internet, that control stops.

---

#### **Question 4 (3.2-D Secure Access)**

Trust Boundary #3 is the "Organizational Ownership Boundary" between Internet and Google. **What controls would you expect Google to place at that boundary that a carrier wouldn't place at theirs? Why?**

**Answer:** I would expect Google to place devices that provide strict control. This is different than carriers because carriers have more traffic and have to focus on getting that connection to proper servers. Google itself has proprietary servers and must be more stringent about who comes in and what they do. Especially because they are offering services rather than just transporting.

**Check:** Excellent insight

- Carrier = **transport provider** (move bits A→B)
- Google = **service provider** (protect their infrastructure and users)
- Google controls at Boundary #3: **WAF (Web Application Firewall)**, load balancers, TLS termination, DDoS protection ([Google Cloud Armor](https://docs.cloud.google.com/armor/docs/security-policy-overview): "Cloud Armor provides a comprehensive list of preconfigured WAF rules based on the OWASP Core Rule Set (CRS) to help you detect SQL injection attacks, cross-site scripting attacks, and other web exploits at the edge of Google's network.")
- Carrier controls at Boundary #2: **firewall/DPI** to protect their network from bad traffic coming back in
- **Key difference:** They have fundamentally different risk models (transport vs. service ownership)
---
## **Security+ Prelab Snapshot**
[[Sub-requirements Matrix]]

| Requirement                             | Status            | Why                                  | Evidence                                  |
| --------------------------------------- | ----------------- | ------------------------------------ | ----------------------------------------- |
| **1.2-A** Confidentiality               | 🔵 Encountered    | Encryption mentioned at TB#1         | Diagram annotation                        |
| **1.2-C** Availability                  | 🔵 Encountered    | Multiple paths, CDN edge servers     | Level 1 diagram                           |
| **1.2-E** Authentication                | 🟡 **Understood** | ✅ Quiz passed                        | Architecture mapping + verbal explanation |
| **1.2-F** Authorization                 | 🟡 **Understood** | ✅ Quiz passed                        | Architecture mapping + verbal explanation |
| **2.2-H** Attack surfaces               | 🔵 Encountered    | Each hop as potential attack surface | Trust boundary mapping                    |
| **3.2-A** Infrastructure considerations | 🟡 **Understood** | ✅ Quiz passed                        | Component differentiation explained       |
| **3.2-C** Secure communication          | 🔵 Encountered    | Encryption at air interface          | Diagram annotations                       |
| **3.2-D** Secure access                 | 🟡 **Understood** | ✅ Quiz passed                        | Organizational boundary analysis          |
| **4.1-D** Wireless security             | 🔵 Encountered    | TB#1 notes wireless exposure         | Diagram annotation                        |


Phase 1.2: [[Segment 1.2 - Level 2 Carrier Architecture]]