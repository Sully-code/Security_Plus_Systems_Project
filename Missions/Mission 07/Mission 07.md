# MISSION PASSPORT

# MISSION: 07 — Move The System To The Cloud

## VERSION: 1.0 — Architecture Draft

## STATUS: Designed / Not Executed

## DESTINATION: CompTIA Security+ V7

---

## 1. DESTINATION

CompTIA Security+ V7

Mission 07 is designed to demonstrate specific Security+ objectives through cloud architecture, identity and access management (IAM), and infrastructure-as-code security. All atomic requirements are accounted for in the Atlas Register. This Passport must align with the master coverage map.

Cost Constraint: All labs executable with 100% free tools (cloud provider free tiers, Terraform, GNS3, open-source security tools).

---

## 2. MISSION INTENT

Understand how to securely migrate and operate systems in cloud environments while managing identity, access, and infrastructure programmatically.

The mission begins with this practical question:

"How do I move an existing system to the cloud securely without introducing unacceptable risks?"

The objective is to develop the ability to:

|Skill|Purpose|
|---|---|
|Design secure cloud architecture|Understand shared responsibility model|
|Implement cloud IAM policies|Least privilege access controls|
|Deploy Infrastructure as Code|Automated, auditable provisioning|
|Protect cloud data storage|Encryption, access controls, backup|
|Configure cloud networking|VPC, security groups, private links|
|Manage identity federation|SSO, MFA, role-based access|
|Monitor cloud resources|Logging, alerting, compliance|
|Assess cloud-specific vulnerabilities|Misconfigurations, exposed services|
|Map demonstrated knowledge to Security+|Produce exam-ready evidence|
|Produce tangible evidence of learning|Portfolio artifacts|

Security+ concepts will be introduced when they become necessary to answer questions about the cloud migration system.

---

## 3. SCENARIO

An organization decides to migrate their on-premises infrastructure (similar to Mission 03's Secure Innovation Lab) to a cloud provider.

Migration path:

`EXISTING ON-PREMISES SYSTEM ↓ CLOUD ASSESSMENT ↓ ARCHITECTURE DESIGN ↓ IDENTITY MIGRATION ↓ INFRASTRUCTURE PROVISIONING (IaC) ↓ NETWORK CONFIGURATION ↓ DATA MIGRATION ↓ SECURITY HARDENING ↓ MONITORING SETUP ↓ VALIDATION & TESTING ↓ OPERATIONAL HANDOVER ↓ SECURITY+ COVERAGE RECORD`

This contrasts with Mission 01 (networking), 02 (satellite), 03 (on-premise infrastructure), 04 (incident response), 05 (app/AI security), and 06 (mobile/drone) by focusing on cloud-native patterns and migration security.

---

## 4. END STATE

Mission 07 is complete when the learner can independently:

|Competency|Evidence Required|
|---|---|
|Design secure cloud architecture|Architecture diagrams with security layers|
|Implement cloud IAM policies|IAM role/policy documentation|
|Deploy Infrastructure as Code|Terraform/CloudFormation scripts|
|Configure cloud networking|VPC, subnet, security group configs|
|Protect cloud data storage|Encryption, access control evidence|
|Implement identity federation|SSO/MFA configuration documentation|
|Monitor cloud resources|CloudWatch/Stackdriver logs analysis|
|Identify cloud-specific vulnerabilities|Misconfiguration scan reports|
|Map demonstrated knowledge to Security+|Coverage matrix update|
|Produce tangible evidence of learning|Portfolio artifacts|
|Explain the complete system coherently|Narrative without script|

---

## 5. WHY THIS MISSION EXISTS

This mission serves specific purposes that Mission 01-06 do not cover:

|Purpose|How Mission 07 Delivers|
|---|---|
|Cloud Architecture Depth|Shared responsibility, regions, zones, services|
|IAM/Identity Federation|SSO, MFA, provisioning, role-based access|
|Infrastructure as Code|Terraform, CloudFormation, automated security|
|Cloud-Native Security|Security groups, WAF, key management|
|Migration Security|Data transfer, hybrid connectivity, cut-over|
|Cloud-Specific Vulnerabilities|Misconfigured buckets, exposed APIs|
|Scalability and Elasticity|Auto-scaling, load balancing security|
|Cloud Provider Agnostic|AWS/Azure/GCP concepts (exam-agnostic)|

Security+ Domain 3.1-B (Cloud Architecture), 4.6 (IAM), and 3.1-F (Infrastructure as Code) all receive primary treatment here.

---

## 6. SYSTEM ARCHITECTURE

Exploration occurs across multiple zoom levels:

### LEVEL 0 — Business View

`ORGANIZATION ↓ CLOUD PROVIDER ↓ SERVICES ↓ USERS`

### LEVEL 1 — Major Cloud Architecture View

`┌─────────────────────────────────────────────────────────┐ │ CLOUD PROVIDER RESPONSIBILITY │ │ • Physical Security │ │ • Hardware │ │ • Network Infrastructure │ │ • Hypervisor │ ├─────────────────────────────────────────────────────────┤ │ CUSTOMER RESPONSIBILITY │ │ • Data Encryption │ │ • Identity & Access │ │ • Network Security Groups │ │ • Operating Systems │ │ • Applications │ └─────────────────────────────────────────────────────────┘`

### LEVEL 2 — Detailed Architecture View

`┌──────────────────────────────────────────────────────────────┐ │ IDENTITY LAYER │ │ • IAM Users/Groups/Roles │ │ • Federated Identity (SSO) │ │ • Multi-Factor Authentication │ │ • Service Accounts │ ├──────────────────────────────────────────────────────────────┤ │ NETWORKING LAYER │ │ • VPC/VNet Configuration │ │ • Public/Private Subnets │ │ • Security Groups/NSGs │ │ • Load Balancers │ │ • PrivateLink/Peering │ ├──────────────────────────────────────────────────────────────┤ │ COMPUTE LAYER │ │ • Virtual Machines │ │ • Containers (Kubernetes/ECS) │ │ • Serverless Functions │ │ • Managed Services │ ├──────────────────────────────────────────────────────────────┤ │ STORAGE LAYER │ │ • Object Storage (S3/Blob) │ │ • Block Storage (EBS/Disk) │ │ • File Storage │ │ • Database Services │ ├──────────────────────────────────────────────────────────────┤ │ MONITORING & GOVERNANCE LAYER │ │ • CloudTrail/Audit Logs │ │ • CloudWatch/Monitoring │ │ • Config/Policy Compliance │ │ • Key Management Service (KMS) │ └──────────────────────────────────────────────────────────────┘`

Key concepts to discover:

- Where does the shared responsibility model divide?
- How do IAM roles minimize privilege?
- What network isolation protects resources?
- How is data encrypted at rest and in transit?
- What logging proves compliance?

### LEVEL 3 — Security Control Stack

`Physical Security (Provider) ↓ Hypervisor (Provider) ↓ Virtual Network (Customer) ↓ Security Groups/ACLs (Customer) ↓ Identity & Access (Customer) ↓ Application Security (Customer) ↓ Data Encryption (Customer)`

Alongside the primary flow:

- Authentication mechanisms (IAM, SSO, MFA)
- Authorization policies (RBAC, ABAC)
- Logging requirements (CloudTrail, audit)
- Encryption key management (KMS, HSM)
- Patch management (customer-managed OS)
- Backup and recovery (snapshots, replication)

### LEVEL 4 — Implementation Components

`┌────────────────────────────────────────────────────────┐ │ CLOUD PROVIDERS (Free Tiers) │ │ • AWS Free Tier │ │ • Google Cloud Free Tier │ │ • Azure Free Account │ │ • Oracle Cloud Free Tier │ ├────────────────────────────────────────────────────────┤ │ INFRASTRUCTURE AS CODE (Free/Open Source) │ │ • Terraform (Open Source) │ │ • Pulumi (Free Tier) │ │ • CloudFormation (AWS Native) │ │ • ARM Templates (Azure Native) │ ├────────────────────────────────────────────────────────┤ │ SECURITY TOOLS (Free/Open Source) │ │ • Checkov/TfSec (IaC Scanning) │ │ • ScoutSuite/CloudSploit (Cloud Scanning) │ │ • Trivy (Container Scanning) │ │ • Cloud Custodian (Policy Automation) │ ├────────────────────────────────────────────────────────┤ │ MONITORING (Free Tiers) │ │ • AWS CloudWatch Free Tier │ │ • Google Cloud Monitoring │ │ • Azure Monitor │ │ • Splunk Free (Log Analysis) │ └────────────────────────────────────────────────────────┘`

### LEVEL 5 — Evidence View

What proves security controls are implemented?

- Terraform/CloudFormation code with security configurations
- IAM policy documents
- Security group rules exports
- Cloud audit logs (CloudTrail, Activity Logs)
- Encryption configuration (KMS keys, bucket policies)
- Vulnerability scan reports (misconfigurations)
- Backup/restore test results
- Identity federation setup documentation
- Network topology diagrams

---

## 7. SYSTEM JOURNEY

The canonical journey for this mission:

`ON-PREMISES ASSESSMENT ↓ CLOUD STRATEGY SELECTION (IaaS/PaaS/SaaS) ↓ ARCHITECTURE DESIGN (Security First) ↓ IDENTITY SETUP (IAM, Federation) ↓ INFRASTRUCTURE PROVISIONING (IaC) ↓ NETWORK CONFIGURATION (VPC, Security Groups) ↓ STORAGE CONFIGURATION (Encryption, Access) ↓ APPLICATION DEPLOYMENT ↓ MONITORING ENABLEMENT ↓ VULNERABILITY SCANNING ↓ COMPLIANCE VALIDATION ↓ CUTOVER PLAN ↓ TESTING & RECOVERY ↓ SECURITY+ COVERAGE RECORD`

This decomposition becomes the investigation framework.

---

## 8. CORE QUESTIONS

### Cloud Architecture

- What cloud model fits this workload (IaaS/PaaS/SaaS)?
- What shared responsibilities apply?
- How are regions and zones selected for resilience?
- What services reduce operational overhead?

### Identity and Access

- How do IAM roles enforce least privilege?
- What is federated identity (SSO)?
- How is MFA enforced for privileged accounts?
- What service accounts need access?
- How do we rotate credentials?

### Infrastructure as Code

- How does IaC enable security consistency?
- What policies validate security pre-deployment?
- How is version control applied to infrastructure?
- What rollback mechanisms exist?

### Networking

- How are VPCs/isolated networks structured?
- What security groups restrict traffic?
- How are public and private subnets separated?
- What connects on-premises to cloud (Direct Connect, ExpressRoute)?

### Data Protection

- How is data encrypted at rest?
- How is data encrypted in transit?
- Who manages encryption keys (customer vs. provider)?
- What backup and retention policies apply?

### Monitoring and Governance

- What logs must be captured for compliance?
- How are alerts configured for security events?
- What tools detect misconfigurations?
- How is audit trail integrity maintained?

### Migration Security

- How is data transferred securely?
- What validates successful migration?
- How do we handle rollback if issues occur?
- What residual risks remain post-migration?

---

## 9. MISSION OPERATING MODEL

Mission 07 follows this cycle:

`ASSESSMENT ↓ DESIGN ↓ IDENTITY SETUP ↓ IAC DEVELOPMENT ↓ DEPLOYMENT ↓ SECURITY HARDENING ↓ MONITORING SETUP ↓ VULNERABILITY ASSESSMENT ↓ VALIDATION ↓ EVIDENCE COLLECTION ↓ SECURITY+ MAPPING`

Mission 07 differs from Mission 01-06 by emphasizing:

- Shared responsibility model (provider vs. customer boundaries)
- Programmatic infrastructure (IaC over manual configuration)
- Identity-centric security (IAM as the perimeter)
- Cloud-native patterns (managed services, elasticity)

---

## 10. SECURITY+ COVERAGE MODEL

Coverage rule (per Atlas): Every Security+ atomic requirement must appear in the Atlas. Mission 07 does not need to own every requirement—it needs to account for each and define its expected contribution.

Coverage status represents expected completion coverage, not learner achievement.

### Status Vocabulary (Mission 07 Completion)

|Status|Meaning|
|---|---|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated|Practical evidence expected from Mission 07|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood|Explanation/application evidence, less implementation|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered|Contextual understanding; deeper ownership elsewhere|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not a Mission 07 Target|Accounted in Atlas; deliberately not owned here|

---

## 11. SECURITY+ ATOMIC COVERAGE TABLE

### DOMAIN 1 — GENERAL SECURITY CONCEPTS

|Requirement|Mission 07 Completion|Rationale|
|---|---|---|
|1.1-A Technical controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Cloud security tools, IAM, encryption|
|1.1-B Preventive controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Security groups, IAM policies|
|1.1-C Managerial controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud governance policies|
|1.1-D Deterrent controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M08 ownership|
|1.1-E Operational controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud operations procedures|
|1.1-F Detective controls|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|CloudTrail, monitoring, alerting|
|1.1-G Physical controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Provider responsibility (M02/M06)|
|1.1-H Corrective controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Auto-healing, failover|
|1.1-I Compensating controls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Alternative controls when ideal unavailable|
|1.1-J Directive controls|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|1.2-A Confidentiality|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Encryption, access controls|
|1.2-B Integrity|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud config validation|
|1.2-C Availability|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Multi-region, auto-scaling|
|1.2-D Non-repudiation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Audit logs, signed requests|
|1.2-E Authentication|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM, SSO, MFA|
|1.2-F Authorization|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM policies, RBAC|
|1.2-G Accounting|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|CloudTrail, billing logs|
|1.2-H Zero Trust|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Identity-centric architecture|
|1.2-I Deception/disruption|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M06 ownership|
|1.3-A Change mgmt processes|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|IaC change workflow|
|1.3-B Technical implications|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Deployment impact analysis|
|1.3-C Change documentation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Git commit history|
|1.3-D Version control|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Terraform state, code repos|
|1.4-A PKI|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Certificate management (ACM/Key Vault)|
|1.4-B Encryption|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|KMS, envelope encryption|
|1.4-C Obfuscation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|1.4-D Hashing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Object integrity checks|
|1.4-E Digital signatures|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|API request signing|
|1.4-F Blockchain|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target|Verification Lab reserved|

### DOMAIN 2 — THREATS, VULNERABILITIES & MITIGATIONS

|Requirement|Mission 07 Completion|Rationale|
|---|---|---|
|2.1-A Nation-state actors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.1-B Unskilled attackers|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Misconfiguration exploitation|
|2.1-C Hacktivists|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.1-D Insider threats|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Admin account abuse|
|2.1-E Organized crime|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M08 ownership|
|2.1-F Shadow IT|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Unauthorized cloud usage|
|2.1-G Data exfiltration|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud storage exposure|
|2.1-H Espionage motivation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.1-I Financial gain motivation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M08 ownership|
|2.2-A Message-based vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05/M08 ownership|
|2.2-B Unsecure network vectors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Exposed security groups|
|2.2-C Social engineering vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|2.2-D File-based vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05 ownership|
|2.2-E Voice call vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M06/M08 ownership|
|2.2-F Supply chain vectors|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud provider risk, marketplace|
|2.2-G Vulnerable software vectors|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M04/M05 ownership|
|2.2-H Attack surfaces|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Cloud services, APIs, storage|
|2.3-A Application vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|2.3-B Hardware vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M02/M04/M06 ownership|
|2.3-C Mobile device vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06 ownership|
|2.3-D Virtualization vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Hypervisor escape concepts|
|2.3-E OS-based vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M04 ownership|
|2.3-F Cloud-specific vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Bucket exposure, IAM misconfigs|
|2.3-G Web-based vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|2.3-H Supply chain vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Marketplace images, dependencies|
|2.4-A Malware attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M05 ownership|
|2.4-B Password attacks|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Credential theft, key rotation|
|2.4-C Application attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|2.4-D Physical attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M02/M03/M06 ownership|
|2.4-E Network attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M02/M03/M04/M06 ownership|
|2.4-F Cryptographic attacks|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M04/M05 ownership|
|2.5-A Segmentation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|VPC, subnet, security groups|
|2.5-B Access control|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM roles, policies, boundary|
|2.5-C Configuration enforcement|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|IaC policies, config rules|
|2.5-D Hardening|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Instance hardening, AMIs|
|2.5-E Isolation|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|VPC peering, private endpoints|
|2.5-F Patching|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Instance/System Manager updates|

### DOMAIN 3 — SECURITY ARCHITECTURE

|Requirement|Mission 07 Completion|Rationale|
|---|---|---|
|3.1-A On-premises architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03 ownership|
|3.1-B Cloud architecture|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Primary focus of mission|
|3.1-C Virtualization architecture|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|VM, container concepts|
|3.1-D IoT architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06 ownership|
|3.1-E ICS architecture|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|Verification Lab reserved|
|3.1-F Infrastructure as Code|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Terraform, CloudFormation|
|3.2-A Infrastructure considerations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Cloud design patterns|
|3.2-B Control selection|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Security tool selection|
|3.2-C Secure communication|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|TLS, private endpoints|
|3.2-D Secure access|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM, private link|
|3.3-A Relevant data types|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M08 ownership|
|3.3-B Data securing methods|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Encryption, tokenization|
|3.3-C Data protection considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Compliance, retention|
|3.3-D Data classifications|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|3.4-A High availability|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Multi-AZ, multi-region|
|3.4-B Site considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Region selection|
|3.4-C Resilience/recovery testing|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|DR drill, backup restore|
|3.4-D Power considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M02/M09 ownership|
|3.4-E Platform diversity|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Multi-cloud concepts|
|3.4-F Backups|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Snapshots, backup services|
|3.4-G Continuity of operations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|

### DOMAIN 4 — SECURITY OPERATIONS

|Requirement|Mission 07 Completion|Rationale|
|---|---|---|
|4.1-A Secure baselines|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|AMI golden images|
|4.1-B Mobile solutions|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M06/M01 ownership|
|4.1-C Hardening|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Instance hardening|
|4.1-D Wireless security|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M01/M02/M06 ownership|
|4.1-E Application security|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05 ownership|
|4.1-F Sandboxing|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M05/M07 partial|
|4.1-G Monitoring computing resources|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|CloudWatch, Stackdriver|
|4.2-A Asset management|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Tagging, inventory|
|4.2-B Asset disposal|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Secure deletion|
|4.2-C Asset assignment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|4.2-D Asset monitoring/tracking|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Resource tagging|
|4.3-A Identify vulnerabilities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Cloud misconfiguration scanning|
|4.3-B Analyze vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Risk prioritization|
|4.3-C Remediate vulnerabilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Fix misconfigurations|
|4.3-D Validate remediation|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Re-scan post-fix|
|4.3-E Report vulnerabilities|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|4.4-A Monitoring tools|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Cloud native monitoring|
|4.4-B Computing resource activities|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Activity logs, metrics|
|4.5-A Firewalls|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Security groups, NACLs|
|4.5-B IDS/IPS|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M04/M07 partial|
|4.5-C DNS filtering|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M04/M05/M07 partial|
|4.5-D DLP|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud DLP services|
|4.5-E NAC|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M07 partial|
|4.5-F EDR/XDR|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M03/M04/M07 partial|
|4.6-A Provisioning|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IAM user/role creation|
|4.6-B SSO|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Identity federation|
|4.6-C MFA|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Enforced authentication|
|4.6-D Privileged access tools|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|Privileged Identity Management|
|4.7-A Automation and Orchestration|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|IaC, auto-scaling|
|4.7-B Scripting benefits|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|CLI, automation scripts|
|4.7-C Automation considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Pipeline security|
|4.8-A Incident response processes|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M09 ownership|
|4.8-B Incident response training|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|
|4.8-C Incident response testing|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M09 ownership|
|4.8-D Root cause analysis|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M09 ownership|
|4.8-E Threat hunting|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud log analysis|
|4.8-F Digital forensics|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud artifact collection|
|4.9-A Log data for investigations|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png)|CloudTrail, VPC Flow Logs|
|4.9-B Other data sources|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Config history, snapshots|

### DOMAIN 5 — SECURITY PROGRAM MANAGEMENT & OVERSIGHT

|Requirement|Mission 07 Completion|Rationale|
|---|---|---|
|5.1-A Guidelines|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud security guidelines|
|5.1-B Policies|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-C Standards|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-D Procedures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-E External considerations|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Provider SLAs, contracts|
|5.1-F Governance monitoring|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Policy compliance (Config)|
|5.1-G Governance structures|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.1-H Roles/responsibilities|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Shared responsibility model|
|5.2-A Risk identification|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud risk assessment|
|5.2-B Risk assessment|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|
|5.2-C Risk analysis|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M02/M04 ownership|
|5.2-D Risk register|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-E Risk tolerance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-F Risk appetite|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-G Risk strategies|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M07/M09 ownership|
|5.2-H Risk reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.2-I BIA|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M09 ownership|
|5.3-A Vendor assessment|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud provider due diligence|
|5.3-B Vendor selection|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-C Vendor agreements|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-D Vendor monitoring|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Continuous compliance|
|5.3-E Vendor questionnaires|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.3-F Rules of engagement|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M08 ownership|
|5.4-A Compliance reporting|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|SOC 2, ISO 27001 evidence|
|5.4-B Non-compliance consequences|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.4-C Compliance monitoring|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Config rules, audits|
|5.4-D Privacy considerations|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M05/M08 ownership|
|5.5-A Attestation|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 + Verification Lab|
|5.5-B Internal audits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.5-C External audits|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 + Verification Lab|
|5.5-D Penetration testing|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M04/M03/M05/M07 partial|
|5.6-A Phishing training|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08 ownership|
|5.6-B Recognize anomalous behavior|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png)|Cloud anomaly detection|
|5.6-C User guidance|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M03/M04 ownership|
|5.6-D User reporting|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04 ownership|
|5.6-E Monitoring|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png)|M08/M04/M03 ownership|

---

## 12. COVERAGE INTEGRITY RESULT

The Atlas Register confirms Mission 07 fills these primary coverage gaps from Mission 01-06:

|Mission 01-06 Weak Area|Mission 07 Strengthens|
|---|---|
|Cloud Architecture|3.1-B Primary|
|IAM/Identity Federation|4.6-A/B/C/D Primary|
|Infrastructure as Code|3.1-F Primary|
|Cloud-Specific Vulnerabilities|2.3-F Primary|
|Cloud Data Protection|3.3-A/B Primary|
|Cloud Monitoring/Logging|4.4-A, 4.9-A Primary|
|Shared Responsibility Model|Core concept|

All orphaned requirements from Mission 01-06 (![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target) remain covered elsewhere in the Atlas.

---

## 13. LABS (FREE TOOLS ONLY)

These are planned labs. Nothing is demonstrated merely because it appears here. All labs use 100% free tools.

|Lab|Objective|Tools|Security+ Links|
|---|---|---|---|
|Lab 01 — Cloud Architecture Design|Design secure cloud architecture with shared responsibility model documented.|[draw.io](http://draw.io/), cloud provider docs|3.1-B, 3.2-A|
|Lab 02 — IAM Policy Development|Create least-privilege IAM policies for users, roles, service accounts.|AWS IAM/Azure AD/GCP IAM|4.6-A/B/C/D, 1.2-E/F|
|Lab 03 — Identity Federation (SSO)|Configure SSO between corporate identity and cloud provider.|AWS SSO, Entra ID|4.6-B, 1.2-E|
|Lab 04 — Infrastructure as Code Deployment|Write Terraform/CloudFormation to provision secure infrastructure.|Terraform, AWS Free Tier|3.1-F, 4.7-A|
|Lab 05 — VPC and Network Configuration|Configure VPC, subnets, security groups, private endpoints.|AWS/VPC, GCP/VNet|2.5-A/E, 3.2-D|
|Lab 06 — Cloud Storage Security|Configure encryption, bucket policies, access controls for storage.|AWS S3, Azure Blob|3.3-B, 1.2-A|
|Lab 07 — Cloud Monitoring Setup|Enable CloudTrail, CloudWatch, configure alerts for security events.|AWS CloudTrail, CloudWatch|4.1-G, 4.9-A|
|Lab 08 — Vulnerability Scanning|Scan cloud environment for misconfigurations.|ScoutSuite, Prowler (free)|4.3-A/B/C/D, 2.3-F|
|Lab 09 — Backup and Recovery Testing|Implement and test backup/restore procedures.|AWS Backup, snapshots|3.4-F, 1.1-H|
|Lab 10 — High Availability Design|Configure multi-AZ/multi-region redundancy.|AWS AZs, Regions|3.4-A, 1.2-C|
|Lab 11 — Secret Management|Store and manage secrets using cloud KMS.|AWS Secrets Manager, KMS|4.6-D, 1.4-B|
|Lab 12 — IaC Security Scanning|Scan Terraform code for security issues before deployment.|Checkov, TfSec|4.3-A, 2.5-C|
|Lab 13 — Incident Response for Cloud|Create playbook for cloud security incidents.|Word Processor (free)|4.8-A, 4.9-A|
|Lab 14 — Compliance Validation|Map cloud configuration to compliance frameworks (SOC 2, ISO).|Compliance frameworks|5.4-A/C|

---

## 14. FAILURE SCENARIOS

|Scenario|Expected Behavior|Investigation Focus|
|---|---|---|
|Failure A — Misconfigured Bucket|Public data exposure|Access policy review|
|Failure B — Overprivileged IAM Role|Excessive permissions|Policy review, least privilege|
|Failure C — Failed Backup Restore|Data loss during recovery|Backup validation process|
|Failure D — Security Group Too Permissive|Unauthorized network access|SG rule audit|
|Failure E — Unencrypted Data|Compliance violation|Encryption verification|
|Failure F — Missing CloudTrail|No audit trail|Logging configuration|

---

## 15. ATTACK SCENARIOS

|Attack Vector|Simulation Approach|Safety Constraints|
|---|---|---|
|Bucket Enumeration|Test own bucket permissions|Own cloud account only|
|Credential Theft Simulation|Practice key rotation, MFA|Own account only|
|Security Group Bypass|Test overly permissive rules|Own VPC only|
|Privilege Escalation|IAM policy misconfiguration testing|Own IAM only|
|API Abuse|Rate limiting on own cloud APIs|Own account only|
|Metadata Service Exploitation|IMDSv2 configuration|Own instances only|

Security Principle: All offensive simulations confined to authorized laboratory environments only (own cloud free tier accounts). No targeting of production systems or third-party services.

---

## 16. TANGIBLE ARTIFACTS

Mission 07 will produce:

|Artifact|Security+ Mapping|
|---|---|
|Cloud Architecture Diagram|3.1-B, 3.2-A|
|IAM Policy Documents|4.6-A/B/C/D|
|SSO/Federation Configuration|4.6-B|
|Terraform/CloudFormation Scripts|3.1-F, 4.7-A|
|VPC/Network Configuration|2.5-A/E, 3.2-D|
|Storage Security Configuration|3.3-B, 1.2-A|
|Cloud Monitoring Dashboard|4.1-G, 4.9-A|
|Misconfiguration Scan Reports|4.3-A/B/C/D, 2.3-F|
|Backup/Restore Test Evidence|3.4-F, 1.1-H|
|HA/DR Design Documentation|3.4-A, 1.2-C|
|Secrets Management Configuration|4.6-D, 1.4-B|
|IaC Security Scan Results|4.3-A, 2.5-C|
|Cloud Incident Response Playbook|4.8-A, 4.9-A|
|Compliance Mapping Document|5.4-A/C|
|Mission 07 Technical Report|Aggregate|
|Security+ Coverage Record|All demonstrated objectives|

---

## 17. EVIDENCE OF LEARNING

Actual learner state tracked separately from planned coverage:

|Planned (Passport)|Actual (Evidence)|
|---|---|
|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated (design intent)|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not encountered (execution pending)|
|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood (design intent)|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered (limited execution)|
|![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) Encountered (design intent)|![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) Understood (partial execution)|
|![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) Not Target|![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) Demonstrated (unexpected success)|
|—|![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png) Exam verified (post-exam)|

---

## 18. SECURITY+ COVERAGE VS. LEARNER STATE

Same principle as Mission 01-06: Planned ≠ Actual.

Execution must produce evidence before awarding demonstrated status.

---

## 19. FAILURE / ATTACK / CHANGE DISCIPLINE

Same cycle as Mission 01-06:

`BASELINE → CHANGE → OBSERVE → DOCUMENT → ANALYZE → RESTORE → VALIDATE`

Plus Cloud Operations:

`PLAN → BUILD → DEPLOY → MONITOR → OPTIMIZE → GOVERN`

---

## 20. OPEN QUESTIONS

|Question|Investigation Path|
|---|---|
|What shared responsibilities apply to each cloud model?|CSP documentation, NIST SP 800-144|
|How do we enforce least privilege in IAM?|AWS IAM Best Practices, NIST guidelines|
|What IaC security gates prevent bad deployments?|Checkov, tfSec, policy-as-code|
|How do we detect cloud misconfigurations?|Cloud security posture management|
|What logging satisfies audit requirements?|Compliance frameworks (SOC 2, ISO)|
|How is cross-account access secured?|IAM roles, cross-account trust|
|What constitutes adequate backup for recovery?|RPO/RTO definitions|
|Which Security+ objectives remain underserved?|Gap analysis|

---

## 21. CURIOSITY BRANCHES

|Branch|Notes|
|---|---|
|Multi-Cloud Architecture|AWS/Azure/GCP comparison|
|Cloud-Native Security Patterns|Well-Architected Frameworks|
|Serverless Security|Lambda/Azure Functions patterns|
|Container Security (EKS/AKS/GKE)|Kubernetes in cloud|
|Cloud Security Posture Management|CSPM tools|
|FinOps and Security|Cost optimization with security|
|Cloud Governance at Scale|Landing zones, guardrails|
|Zero Trust in Cloud|Beyond traditional perimeter|

---

## 22. DEFERRED TOPICS

|Topic|Reason Deferred|
|---|---|
|Deep Cloud Provider Specifics|AWS/Azure/GCP beyond Security+ scope|
|Enterprise IAM Complexity|M08 ownership|
|Advanced Cryptographic Implementation|M01/M05/M07 partial|
|Industrial Control Systems|Verification Lab|
|Blockchain Implementation|Verification Lab|
|Business Continuity Planning|M09 ownership|
|Third-Party Risk Management|M08 ownership|
|Deep Legal/Compliance Frameworks|M08 ownership|

---

## 23. PRESSURE-TEST FINDINGS

Strong coverage areas:

- Cloud Architecture (3.1-B Primary)
- IAM/Identity Federation (4.6-A/B/C/D Primary)
- Infrastructure as Code (3.1-F Primary)
- Cloud-Specific Vulnerabilities (2.3-F Primary)
- Cloud Data Protection (3.3-B)
- Cloud Monitoring/Logging (4.4-A, 4.9-A)
- Shared Responsibility Model (Core concept)
- Free Tool Compatibility (Cloud free tiers + open-source tools)

Natural crossover with Mission 03 (Infrastructure), 05 (App Security), 06 (Mobile/Drone backend), and 08 (Governance) provides reinforcement without duplication.

---

## 24. WHAT THE PRESSURE TEST REJECTED

Mission 07 will not artificially expand to demonstrate:

- Enterprise Security Architecture (M03)
- Incident Response Lifecycle (M04)
- Application Development Security (M05)
- Mobile/Wireless Security (M01/M02/M06)
- Governance/Risk Management Depth (M08)
- Business Continuity Planning (M09)
- Blockchain (Verification Lab)
- ICS Architecture (Verification Lab)

---

## 25. NEXT MISSION CONNECTIONS

|Future Mission|Connection Points|
|---|---|
|Mission 08 — System Nobody Understands|Governance oversight of cloud programs|
|Mission 09 — Everything Is Failing|Disaster recovery for cloud systems|

Mission 07 establishes cloud security rigor that later missions reference for governance and resilience.

---

## 26. CURRENT STATE

|Item|Status|
|---|---|
|Mission status|Not started|
|Architecture|Defined at conceptual level|
|Security+ coverage design|Aligned with Atlas|
|Atomic requirements|All accounted|
|Planned completion coverage|Defined|
|Labs|Designed, not executed|
|Artifacts|None produced yet|
|Security+ evidence|None yet|
|Learner state|Not pre-awarded|
|Lab cost|$0 (cloud free tiers + open-source)|

---

## 27. WHAT WE KNOW

At mission launch, we know the intended architecture and learning objectives. We do not assume paper architecture equals demonstrated knowledge.

---

## 28. WHAT WE HAVE BUILT

Architecture and learning design complete. Laboratory implementation pending. First artifact will be cloud architecture diagram.

---

## 29. NEXT RECOMMENDED ACTION

Begin with Level 0 → Level 1 Architecture Design. First question:

"What are the three cloud service models, and how does security responsibility differ for each?"

That question determines the first conceptual branch.

---

## 30. MISSION COMPLETE WHEN

Mission 07 is complete only when:

- Cloud architecture diagrams produced
- IAM policies configured and tested
- SSO/federation set up
- IaC scripts written and scanned
- VPC/networking configured
- Storage security implemented
- Cloud monitoring operational
- Misconfiguration scans run
- Backup/restore tested
- HA/DR validated
- Secrets managed securely
- Incident response playbook created
- Compliance mapping documented
- Tangible artifacts assembled
- Security+ evidence recorded
- Remaining gaps identified
- Uncovered objectives assigned to later missions or Verification Labs

---

## 31. HANDOFF NOTES FOR ANOTHER AI

Do not restart this mission from scratch. The learner uses a systems-journey learning model. Destination is CompTIA Security+ V7.

Key reminders:

- Do not turn this into a cloud certification course (AWS/Azure/GCP specific)
- Focus on Security+ objectives, not vendor-specific certification
- Require evidence before awarding demonstrated status
- Preserve coverage integrity per Atlas Register
- Use Verification Labs for orphaned objectives (Blockchain, ICS, attestation)
- Maintain all labs at $0 cost (cloud free tiers, open-source tools)
- Keep offensive activities isolated to own cloud accounts
- Cloud concepts are provider-agnostic (exam requirement)

Governing principle: Security+ is the destination. The Mission Atlas is the vehicle.

---

## 32. ARCHITECTURAL FREEZE

Incorporating Atlas Register frozen principles:

|Principle|Applied to Mission 07|
|---|---|
|Every Security+ requirement represented in Atlas|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Coverage table maps all|
|Passport uses atomic Security+ coverage|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Table uses 1.1-A through 5.6-E|
|Coverage = intended completion, not current|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Distinction maintained|
|Four planning classes (![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png))|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Applied throughout|
|Five-state learner vocabulary (![⚪](https://fonts.gstatic.com/s/e/notoemoji/17.0/26aa/32.png) ![🔵](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f535/32.png) ![🟡](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e1/32.png) ![🟢](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e2/32.png) ![🟣](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f7e3/32.png))|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Separate from planned|
|Mission ownership ≠ Atlas coverage|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Reinforcement tracked|
|No artificial expansion|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Rejected items listed|
|Verification Labs for gaps|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Blockchain, ICS reserved|
|4.8 IR + 4.9 Data Sources separate|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Maintained in coverage table|
|Labs planned until executed|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) All labs marked planned|
|Artifacts not produced until existing|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) Zero artifacts currently|
|Labs must be 100% free|![✅](https://fonts.gstatic.com/s/e/notoemoji/17.0/2705/32.png) All labs use cloud free tiers + open-source|