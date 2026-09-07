## LAB 09 — Vulnerability Lifecycle

### Objective

Take a deliberately introduced vulnerability through the complete lifecycle: Identify → Analyze → Remediate → Validate → Report. This lab exists specifically to ensure 4.3 is not reduced to "run a scanner."

### Security+ Atomic Coverage

|ID|Requirement|Coverage Level|Evidence Produced|
|---|---|---|---|
|4.3-A|Identify vulnerabilities|🟢 Demonstrated|Vulnerability identified via scan AND manual verification|
|4.3-B|Analyze vulnerabilities|🟢 Demonstrated|CVSS scoring, exploitability analysis, impact assessment|
|4.3-C|Remediate vulnerabilities|🟢 Demonstrated|Vulnerability patched/fixed in the lab|
|4.3-D|Validate remediation|🟢 Demonstrated|Re-scan confirms vulnerability is resolved|
|4.3-E|Report vulnerabilities|🟢 Demonstrated|Formal vulnerability report produced|
|4.1-A|Secure baselines|🟢 Demonstrated|Baseline configuration applied post-remediation|
|2.5-F|Patching|🟡 Understood|Patching process understood (simulated where real patching isn't applicable)|
|1.3-B|Technical implications of changes|🟢 Demonstrated|Change → remediation → validation documented|

### Prerequisites

Labs 02 and 07 complete.

### Tools

- Ubuntu Server VM (target machine)
- Nmap (scanner)
- OpenVAS / Greenbone (vulnerability scanner) — or Nmap NSE scripts as a lighter alternative
- Text editor / markdown for report

### Environment Setup

Set up an intentionally vulnerable target:

1. Deploy an Ubuntu Server VM in VirtualBox.
2. Install an older, intentionally vulnerable service. For example:

`# Install a web server with an intentionally outdated configuration sudo apt update sudo apt install apache2 # Enable directory listing (vulnerability) sudo nano /etc/apache2/apache2.conf # Add: Options +Indexes to the <Directory /var/www/> block sudo systemctl restart apache2`

Alternatively, download and run a deliberately vulnerable application in Docker:

`# Option: DVWA (Damn Vulnerable Web Application) docker run -d -p 8080:80 vulnerables/web-dvwa`

### Procedure

**Step 1 — IDENTIFY**

**1a. Port scan to discover attack surface:**

`nmap -sV -p- <target-IP>`

Document:

- Open ports
- Service versions identified
- OS detection (if available)

**1b. Vulnerability scan:**

Using Nmap NSE scripts (lightweight):

`nmap -sV --script vuln <target-IP>`

Or using OpenVAS/Greenbone (more comprehensive):

1. Start Greenbone: `sudo gvm-start`
2. Access the web interface at `https://127.0.0.1:9392`
3. Create a new scan task targeting the vulnerable VM.
4. Run the scan and wait for results.

Document:

- What vulnerabilities were found
- Their severity ratings
- Whether they were found by automated scanning alone or required manual verification

**1c. Manual verification:**

For at least one finding, manually verify the vulnerability:

- If directory listing is enabled: open a browser and navigate to `http://<target-IP>/` — can you see a file listing?
- If DVWA is running: attempt to access it and note the default credentials.

Document: What did the scanner find that manual verification confirmed? Did the scanner miss anything you found manually?

**Step 2 — ANALYZE**

For each identified vulnerability:

**2a. Classify the vulnerability:**

- Type (misconfiguration, outdated software, weak credentials, etc.)
- CVSS score (look up if the scanner provides it, or assess qualitatively)
- Exploitability: How easy would this be to exploit?
- Impact: What would a successful exploitation allow?

**2b. Determine the root cause:**

- Is it a configuration error?
- Is it an outdated package?
- Is it a design flaw in the application?
- Is it a missing security control?

Create a table:

|Finding|Type|Severity|Root Cause|Exploitability|
|---|---|---|---|---|
|Directory listing enabled|Misconfiguration|Medium|Apache config allows Indexes|Easy — browse to URL|
|Default DVWA credentials|Weak credentials|High|Application ships with admin/password|Easy — attempt login|

**Step 3 — REMEDIATE**

Fix each vulnerability:

**3a. Fix directory listing:**

`sudo nano /etc/apache2/apache2.conf # Change Options +Indexes to Options -Indexes sudo systemctl restart apache2`

**3b. Fix default credentials:**

- Change the DVWA admin password via the application interface.

**3c. Additional hardening:**

- Disable unnecessary modules: `sudo a2dismod autoindex`
- Verify file permissions: `ls -la /var/www/html/`

Document each remediation action and why it resolves the vulnerability.

**Step 4 — VALIDATE**

**4a. Re-scan:**

`nmap -sV --script vuln <target-IP>`

Or re-run the OpenVAS scan.

Document: Are the previous findings gone? Were any new issues introduced by the remediation?

**4b. Manual validation:**

- Browse to `http://<target-IP>/` — is the directory listing gone?
- Attempt to log in with old credentials — does it fail?

**4c. Document the before/after:**

|Finding|Pre-Remediation|Post-Remediation|
|---|---|---|
|Directory listing|Visible|Returns 403 Forbidden|
|Default credentials|Login succeeds|Login fails|

**Step 5 — REPORT**

Produce a formal vulnerability report containing:

`# Vulnerability Assessment Report ## Executive Summary [Brief overview of what was scanned, what was found, and what was remediated] ## Scope - Target: [IP address / system] - Scan date: [date] - Tools used: Nmap, OpenVAS ## Findings ### Finding 1: [Title] - **ID:** VULN-001 - **Severity:** [Critical/High/Medium/Low] - **Description:** ... - **Evidence:** [scan output, screenshot] - **Root Cause:** ... - **Remediation:** ... - **Validation:** [re-scan result] - **Status:** Resolved ### Finding 2: ... ## Residual Risk [Any issues that could not be remediated and why] ## Recommendations [Long-term recommendations]`

Save as `mission01-lab09-vuln-report.md`.

### Artifacts Produced

|Artifact|Passport Reference|
|---|---|
|Initial scan results (Nmap + OpenVAS)|Vulnerability lifecycle evidence|
|Vulnerability analysis table|Vulnerability lifecycle evidence|
|Remediation action log|Vulnerability lifecycle evidence|
|Validation re-scan results|Vulnerability lifecycle evidence|
|Formal vulnerability report|Vulnerability lifecycle evidence|

### Success Criteria

- At least one vulnerability went through the complete lifecycle: identify → analyze → remediate → validate → report
- The scanner alone was not the only identification method — manual verification occurred
- Remediation was validated through re-scanning AND manual testing
- Formal report follows a professional structure
- Learner can explain why "running a scanner" alone does not satisfy vulnerability management

### Curiosity Branches

- What is the CVSS (Common Vulnerability Scoring System)?
- How does CVE (Common Vulnerabilities and Exposures) numbering work?
- What is the difference between vulnerability scanning and penetration testing?