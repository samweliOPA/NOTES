# 🏛️ GRC & CIS Controls: The Framework for a Secure Organization
### *A SOC Analyst's Complete Field Guide*

> *"Security without governance is chaos. Governance without security is theater. GRC and CIS Controls together make security real, measurable, and defensible."*

---

## 📋 Table of Contents

1. [What Is GRC?](#1-what-is-grc)
2. [The Three Pillars of GRC](#2-the-three-pillars-of-grc)
3. [Why GRC Matters to a SOC Analyst](#3-why-grc-matters-to-a-soc-analyst)
4. [Introduction to CIS Controls](#4-introduction-to-cis-controls)
5. [CIS Controls v8 — All 18 Controls Explained](#5-cis-controls-v8--all-18-controls-explained)
6. [CIS Implementation Groups (IG1, IG2, IG3)](#6-cis-implementation-groups-ig1-ig2-ig3)
7. [How a SOC Analyst Works Within GRC & CIS](#7-how-a-soc-analyst-works-within-grc--cis)
8. [GRC Frameworks: The Bigger Picture](#8-grc-frameworks-the-bigger-picture)
9. [Risk Management — The Heart of GRC](#9-risk-management--the-heart-of-grc)
10. [Compliance Mapping — CIS to Other Frameworks](#10-compliance-mapping--cis-to-other-frameworks)
11. [GRC Tools a SOC Analyst Should Know](#11-grc-tools-a-soc-analyst-should-know)
12. [SOC Analyst Daily Touchpoints with GRC](#12-soc-analyst-daily-touchpoints-with-grc)
13. [Metrics & Reporting for SOC Within GRC](#13-metrics--reporting-for-soc-within-grc)
14. [Building & Maturing a GRC Program](#14-building--maturing-a-grc-program)
15. [Common GRC Mistakes and How to Avoid Them](#15-common-grc-mistakes-and-how-to-avoid-them)
16. [SOC Analyst Notes & Quick Reference](#16-soc-analyst-notes--quick-reference)
17. [Glossary](#17-glossary)

---

## 1. What Is GRC?

**GRC** stands for **Governance, Risk, and Compliance**. It is the integrated framework that organizations use to:

- Set strategic direction and policies (Governance)
- Identify, assess, and manage threats to the organization (Risk)
- Meet legal, regulatory, and industry obligations (Compliance)

GRC is **not a product** — it is a discipline, a culture, and a set of processes. It is the operating system of an organization's security program.

### The Simple Mental Model

```
Without GRC:
  Security = Ad-hoc firefighting, no strategy, no accountability

With GRC:
  Security = Deliberate, measurable, aligned to business objectives
```

### GRC Is About One Core Question

> *"Are we doing the right things, in the right way, for the right reasons — and can we prove it?"*

- **Right things** → Governance (policies, strategy)
- **Right way** → Risk Management (controls, threat response)
- **Right reasons** → Compliance (laws, regulations, standards)
- **Prove it** → Audit, evidence, documentation

---

## 2. The Three Pillars of GRC

### Pillar 1: Governance

**Governance** is the structure of rules, practices, and processes by which an organization is directed and controlled from a security perspective.

**What governance includes:**

| Component | Description |
|-----------|-------------|
| **Security Policies** | Written rules that define expected behavior (e.g., Acceptable Use Policy, Password Policy) |
| **Standards** | Mandatory specifications to support policies (e.g., "Passwords must be 12+ characters") |
| **Procedures** | Step-by-step operational instructions (e.g., incident response playbooks) |
| **Guidelines** | Recommended but not mandatory practices |
| **Roles & Responsibilities** | Who owns what security decision (CISO, SOC, IT, Business) |
| **Security Strategy** | Long-term security roadmap aligned with business goals |

**Governance documents every SOC analyst should know:**

- **Information Security Policy** — The master document
- **Incident Response Policy** — When/how to escalate incidents
- **Acceptable Use Policy (AUP)** — What employees can/cannot do
- **Data Classification Policy** — How data is categorized (Public, Internal, Confidential, Restricted)
- **Access Control Policy** — Who gets access to what and how
- **Change Management Policy** — How changes to systems are approved

> 📌 **SOC Analyst Note:** When you respond to an incident, governance tells you *what you are authorized to do*, who to notify, and what constitutes a breach. Always know your IR policy before an incident happens — not during one.

---

### Pillar 2: Risk Management

**Risk management** is the process of identifying threats and vulnerabilities, assessing their potential impact, and making deliberate decisions about how to handle them.

**The Risk Formula:**

```
Risk = Threat × Vulnerability × Impact

  Threat       = Something that could cause harm (attacker, disaster, insider)
  Vulnerability = A weakness that could be exploited
  Impact       = The damage if the threat materializes
```

**Risk Treatment Options:**

| Option | Description | Example |
|--------|-------------|---------|
| **Mitigate** | Reduce the risk with controls | Deploy MFA to reduce account takeover risk |
| **Accept** | Acknowledge and tolerate the risk | Accept risk of legacy software for 6 more months |
| **Transfer** | Shift the financial risk to another party | Buy cyber insurance |
| **Avoid** | Stop the activity that creates the risk | Don't collect data you don't need |

**The Risk Register:**
A risk register is a living document that tracks all identified risks with their owner, current rating, treatment, and status. As a SOC analyst, your incident data feeds the risk register — your detections reveal real threats materializing.

> 📌 **SOC Analyst Note:** Every significant incident you handle is evidence of a risk materializing. Document your findings well — they update the organization's risk register and influence investment in new controls.

---

### Pillar 3: Compliance

**Compliance** is the process of ensuring the organization adheres to external laws, regulations, standards, and contractual obligations.

**Types of compliance drivers:**

| Type | Examples |
|------|---------|
| **Legal/Regulatory** | GDPR, HIPAA, PCI DSS, SOX, CCPA |
| **Industry Standards** | ISO 27001, NIST CSF, CIS Controls |
| **Contractual** | Customer security requirements, vendor agreements |
| **Internal** | Your own policies and procedures |

**Compliance does NOT equal Security.**

An organization can be **compliant but insecure** (meets PCI DSS requirements but has poor real-world security) or **secure but non-compliant** (excellent security that doesn't align with a standard's specific checklist). CIS Controls go beyond compliance — they focus on what actually works against real attackers.

> 📌 **SOC Analyst Note:** Use compliance as the floor, not the ceiling. CIS Controls build the house above the foundation that compliance sets.

---

## 3. Why GRC Matters to a SOC Analyst

Many SOC analysts think GRC is just for managers and auditors. This is wrong. GRC directly shapes your daily work:

| GRC Element | How It Affects the SOC Analyst |
|-------------|-------------------------------|
| **Incident Response Policy** | Defines escalation paths, notification requirements, and your authority during incidents |
| **Data Classification Policy** | Tells you how to handle evidence — what can leave the org, what must be retained |
| **Asset Inventory (CIS Control 1)** | Without this, you're investigating incidents on systems you know nothing about |
| **Log Management Policy** | Determines what logs you have access to and retention period |
| **Change Management** | Helps distinguish authorized changes from malicious modifications |
| **Risk Register** | Tells you which assets are high-value targets to prioritize in monitoring |
| **Compliance Requirements** | Dictate breach notification timelines (GDPR: 72 hours; HIPAA: 60 days) — you must know these |

GRC is the rulebook you operate under. The better you understand it, the more effective and defensible your work becomes.

---

## 4. Introduction to CIS Controls

### What Are CIS Controls?

The **CIS Controls** (formerly SANS Top 20 / Critical Security Controls) are a prioritized set of cybersecurity best practices developed by the **Center for Internet Security (CIS)**. They represent a community-consensus effort from cybersecurity experts worldwide.

**Current version:** CIS Controls **v8** (released May 2021)

They were created by studying how real attackers breach real organizations and working backwards to define what defenses would stop them:

> *"Offense informs defense — start with what attackers actually do, then define the controls that would have stopped them."*

### CIS Controls vs. Other Frameworks

| Framework | Focus | Best For |
|-----------|-------|----------|
| **CIS Controls** | Specific, tactical, technical controls | Practitioners — what to *do* |
| **NIST CSF** | Risk-based framework, broad categories | Strategy and risk communication |
| **ISO 27001** | Information security management system | Certification, auditors |
| **NIST 800-53** | Comprehensive control catalog | Government and highly regulated industries |

CIS Controls map to all of these, making them the best starting point for any organization regardless of which framework they must ultimately comply with.

---

## 5. CIS Controls v8 — All 18 Controls Explained

CIS v8 organizes controls into three categories:

- **Basic Cyber Hygiene (Controls 1–6)** — Foundational controls every organization must have
- **Foundational Security (Controls 7–16)** — The next layer of defense
- **Organizational Controls (Controls 17–18)** — People and program-level controls

---

### BASIC CYBER HYGIENE

---

### Control 1: Inventory and Control of Enterprise Assets

**What it is:** Know every hardware asset connected to your network.

**Why it matters:** You cannot defend what you don't know exists. Attackers find and exploit unknown, forgotten, and unmanaged assets — shadow IT, rogue devices, forgotten servers. These are the gaps they walk through.

**Key safeguards:**
- Maintain an up-to-date inventory of all enterprise assets (servers, workstations, network devices, mobile, IoT, cloud instances)
- Use active discovery (network scanning) and passive discovery (DHCP logs, NAC)
- Immediately address unauthorized assets — block or remediate

**SOC Analyst Role:**
- When an alert fires, the asset inventory tells you what the system is, who owns it, its criticality, and what it connects to
- Alert on assets appearing on the network that are NOT in inventory — unauthorized devices are a red flag for attacker persistence, rogue devices, or insider threat
- Cross-reference every alert with the asset inventory before assessing severity

> 📌 **SOC Note:** If your SIEM fires for a new IP/hostname and it doesn't appear in your CMDB, treat it as a potential security incident until proven otherwise. "Unknown asset = potential threat" is the correct default assumption.

---

### Control 2: Inventory and Control of Software Assets

**What it is:** Know every piece of software running in your environment — and only allow authorized software to run.

**Why it matters:** Unauthorized or unknown software may be malware, shadow IT, or vulnerable applications that attackers can exploit.

**Key safeguards:**
- Maintain a software inventory (including version numbers)
- Use application allowlisting to prevent unauthorized software execution
- Remove unauthorized and unsupported software
- Block execution of software not in the approved list

**SOC Analyst Role:**
- Application allowlisting alerts (unauthorized process execution) are direct SOC detections tied to this control
- When malware is detected, the software inventory helps determine if it's a known tool or an unknown binary
- Software inventory gaps = detection blind spots

> 📌 **SOC Note:** One of the most powerful detections you can build is alerting on processes executing that are NOT in your approved software baseline. Sysmon Event ID 1 (Process Creation) + a SIEM rule against a process allowlist = instant detection of unauthorized execution.

---

### Control 3: Data Protection

**What it is:** Identify, classify, and protect sensitive data throughout its lifecycle.

**Why it matters:** Data is what attackers ultimately want. If you don't know where your sensitive data lives, you can't protect it or detect when it's stolen.

**Key safeguards:**
- Establish a data classification scheme (e.g., Public, Internal, Confidential, Restricted)
- Encrypt sensitive data at rest and in transit
- Implement Data Loss Prevention (DLP) tools
- Retain data only as long as required (data minimization)
- Establish secure data disposal procedures

**SOC Analyst Role:**
- DLP alerts are directly tied to this control — you investigate when sensitive data moves in unexpected ways
- Detecting unusual exfiltration (large uploads, email attachments to external addresses, USB activity) is a core SOC function
- When investigating a potential breach, encryption status determines severity — was the stolen data encrypted?

> 📌 **SOC Note:** Know your data classification policy cold. When a potential breach occurs, the first question leadership asks is: "Was it sensitive data?" Your ability to answer that correctly — and quickly — determines the severity of your response and your regulatory obligations.

---

### Control 4: Secure Configuration of Enterprise Assets and Software

**What it is:** Establish and maintain secure configurations for all hardware and software assets.

**Why it matters:** Default configurations are designed for usability, not security. Open ports, default credentials, unnecessary services — all create attack surface that adversaries actively exploit.

**Key safeguards:**
- Use CIS Benchmarks as your secure configuration standard (free, downloadable from cisecurity.org)
- Establish secure configuration baselines for each OS and application type
- Use configuration management tools to enforce baselines and detect drift
- Disable unnecessary ports, services, and protocols
- Change all default credentials immediately upon deployment

**SOC Analyst Role:**
- Configuration drift alerts indicate systems are no longer in their secure baseline — could be attacker modification or admin error, both require investigation
- During incident investigation, compare the current system configuration against the secure baseline — attackers commonly modify configurations (disable AV, open firewall ports, add new services)
- Tools: CIS-CAT scanner, Tenable.sc benchmarks, SCAP-compliant assessment tools

> 📌 **SOC Note:** A common attacker technique (MITRE ATT&CK T1562 — Impair Defenses) is to disable logging, turn off AV, or remove firewall rules. If you detect configuration changes to security tools — especially outside a change window — escalate immediately. This is one of the highest-priority signals of an active attacker.

---

### Control 5: Account Management

**What it is:** Manage user and administrator accounts throughout their lifecycle — creation, use, and deletion.

**Why it matters:** Compromised accounts are the #1 initial access vector. Orphaned accounts, excessive privilege, and shared credentials are prime targets. An attacker with valid credentials looks like a legitimate user.

**Key safeguards:**
- Maintain an inventory of all accounts (user, admin, service, shared, system)
- Disable dormant accounts after a defined inactivity period
- Remove accounts immediately when employees leave (offboarding process)
- Restrict use of administrative accounts (don't use admin accounts for daily tasks)
- Require unique accounts — no shared passwords

**SOC Analyst Role:**
- Authentication failures, impossible travel logins, logins from new locations — all account-based detections
- Investigate dormant accounts showing activity — a key indicator of account compromise or insider threat
- During investigations, account timeline analysis is critical: when was the account created, when was it last used, have privileges changed?

> 📌 **SOC Note:** Key Windows Event IDs for account investigations:
> - `4720` — Account created
> - `4728` / `4732` — Added to privileged group (Domain Admins, Local Admins)
> - `4625` — Failed logon
> - `4648` — Logon using explicit credentials (pass-the-hash indicator)
> - `4740` — Account locked out

---

### Control 6: Access Control Management

**What it is:** Use processes and tools to create, assign, manage, and revoke access credentials — enforcing the principle of least privilege.

**Why it matters:** Overprivileged users create massive blast radius when compromised. Least privilege limits what an attacker can do even after gaining access.

**Key safeguards:**
- Enforce **Least Privilege** — only the minimum access needed for each role
- Implement **Role-Based Access Control (RBAC)**
- Require **Multi-Factor Authentication (MFA)** for all accounts — especially privileged and remote access
- Separate administrative accounts from regular user accounts
- Conduct regular access reviews and recertification
- Implement Privileged Access Management (PAM) for administrative access

**SOC Analyst Role:**
- MFA bypass attempts, privilege escalation events, and lateral movement are all detections tied to this control
- Unauthorized privilege escalation (e.g., standard user suddenly appearing in Domain Admins) is a critical P1 alert
- PAM solutions provide logs of privileged sessions — vital for investigations involving admin-level compromise

> 📌 **SOC Note:** MFA is your single most powerful control against account takeover. A user successfully authenticating without MFA in an MFA-enforced environment is a critical anomaly — investigate immediately. Monitor Event ID 4672 (Special Logon — administrative privileges assigned at logon) as an early indicator of privilege abuse.

---

### FOUNDATIONAL SECURITY

---

### Control 7: Continuous Vulnerability Management

**What it is:** Continuously find, assess, and remediate vulnerabilities across your environment.

**Why it matters:** Attackers scan for and exploit known vulnerabilities. The longer a vulnerability is unpatched, the higher the probability it will be exploited. The patch gap is an open invitation.

**Key safeguards:**
- Conduct vulnerability scanning at least weekly (continuously for critical systems)
- Use authenticated scans for complete and accurate coverage
- Prioritize remediation based on real risk (CVSS + exploitability + asset criticality)
- Establish SLAs for patch remediation by severity tier
- Track and report patch compliance metrics

**SOC Analyst Role:**
- Vulnerability data enriches incident investigations — when a system is compromised, immediately check vulnerability scan data for open CVEs on that host
- Your SIEM should ingest vulnerability data so alerts on highly vulnerable systems get auto-elevated in priority
- IDS/IPS signatures are written for specific CVEs — understanding vulnerabilities helps you tune your detections

> 📌 **SOC Note:** Cross-reference every compromised host with vulnerability scan data during IR. The CVEs on that system often point directly to the initial access vector. This turns forensics from guesswork into evidence-based analysis. "The attacker exploited CVE-XXXX-XXXX" is far more useful in a report than "the attacker used an unknown method."

---

### Control 8: Audit Log Management

**What it is:** Collect, protect, and analyze audit logs from all systems to support detection, investigation, and compliance.

**Why it matters:** Logs are the foundation of everything the SOC does. No logs = no visibility = no detection = no investigation. Attackers know this and target logging infrastructure to cover their tracks.

**Key safeguards:**
- Collect logs from all enterprise assets: systems, network devices, cloud, applications
- Centralize logs in a SIEM or log management platform
- Retain logs for sufficient periods (90 days minimum hot storage, 1 year archive — check your compliance requirements)
- Protect log integrity — logs must not be modifiable by regular users or compromised systems
- Standardize timestamps (use UTC across all sources)

**Critical Log Sources:**

| Source | What It Gives You |
|--------|------------------|
| Windows Event Logs | Authentication, process execution, account changes, service installs |
| Sysmon | Deep process, network, file, and registry telemetry |
| Firewall Logs | Network connections, blocked traffic, rule changes |
| DNS Logs | Hostname lookups — detect C2 beaconing and DGA patterns |
| Proxy/Web Logs | Web traffic, malicious downloads, data exfiltration |
| EDR Telemetry | Endpoint process trees, lateral movement, behavioral detections |
| Cloud Logs (CloudTrail, Azure Monitor) | Cloud resource access, API calls, configuration changes |
| Authentication Logs (AD, SSO, MFA) | Login patterns, MFA bypass attempts, failed authentications |

**SOC Analyst Role:**
- Logs ARE your job. Everything you do depends on log quality and availability
- Monitor log source health — a source going silent may indicate tampering or infrastructure failure
- Build detection rules based on what should appear in logs (anomaly-based) and known-bad patterns (signature-based)

> 📌 **SOC Note:** The first thing many attackers do after gaining access is attempt to clear logs. These are automatic P1 alerts:
> - `Event ID 1102` — Security Audit Log Cleared
> - `Event ID 104` — System Log Cleared
>
> Log clearing almost certainly means an active attacker is present and trying to hide their tracks. Drop everything and respond.

---

### Control 9: Email and Web Browser Protections

**What it is:** Improve protections and detections for email and web browsing — the two most common attack delivery channels.

**Why it matters:** Phishing email is the #1 initial access vector. Drive-by downloads via browser are #2. This control protects the entry points attackers exploit most frequently.

**Key safeguards:**
- Deploy email filtering with anti-phishing, anti-spam, and malware scanning
- Implement **DMARC, DKIM, and SPF** to prevent email domain spoofing
- Use a DNS-based web filter or Secure Web Gateway (SWG) to block malicious domains
- Block dangerous attachment file types in email
- Enable browser sandboxing and keep browsers updated
- Block unnecessary browser plugins/extensions

**SOC Analyst Role:**
- Phishing alerts from the email gateway are Tier 1 SOC bread and butter — suspicious links, known-bad senders, malicious attachment detections
- Monitor DNS query logs for communication to newly registered domains, known C2 infrastructure, and domain generation algorithm (DGA) patterns
- When users report phishing: determine whether anyone clicked, whether malware executed, and whether the sender is known-bad

> 📌 **SOC Note:** Check if your organization has DMARC set to `p=reject`. If it's `p=none`, attackers can spoof your domain in phishing campaigns against your customers and partners. This is a governance gap worth escalating to the GRC team — it's a reputational and legal risk, not just a technical one.

---

### Control 10: Malware Defenses

**What it is:** Control the installation, spread, and execution of malicious code across the environment.

**Why it matters:** Malware remains a primary tool of attackers — ransomware, RATs, keyloggers, wipers. Defense requires multiple overlapping layers, not just a single antivirus product.

**Key safeguards:**
- Deploy Endpoint Detection and Response (EDR) on all endpoints
- Enable anti-exploitation features (DEP, ASLR, Exploit Guard)
- Use application allowlisting (ties back to Control 2)
- Centralize malware detection events to SIEM
- Implement DNS filtering to block C2 communication
- Scan removable media before allowing connection

**SOC Analyst Role:**
- EDR alerts are your primary malware detection source — investigate process trees, parent-child relationships, and network connections from suspicious processes
- Malware triage workflow: Identify → Contain → Eradicate → Recover → Document
- Use sandboxing tools (Any.run, Joe Sandbox, Cuckoo) to analyze suspicious files safely without running them on production systems

> 📌 **SOC Note:** EDR is far superior to legacy AV for SOC investigations. Signature-based AV tells you "malware found." EDR tells you the full story — the parent process that launched it, every file it touched, every network connection it made, every registry key it modified. If your org still uses only legacy AV, advocate for EDR. The difference in investigation capability is enormous.

---

### Control 11: Data Recovery

**What it is:** Establish and maintain data recovery practices sufficient to restore affected systems to their pre-incident state.

**Why it matters:** Ransomware's leverage is destroying your ability to recover. Solid, protected backups eliminate that leverage. Recovery capability also determines how quickly you restore operations after any incident.

**Key safeguards:**
- Follow the **3-2-1 backup rule:** 3 copies, 2 different media types, 1 offsite or offline
- Test backups regularly — an untested backup may not work when needed
- Protect backups from ransomware using immutable backups and air-gapped copies
- Include cloud data in backup scope
- Define and document Recovery Time Objective (RTO) and Recovery Point Objective (RPO)

**SOC Analyst Role:**
- During ransomware incidents, your first question should be: "Are backups clean and available?"
- Verify backup infrastructure was not compromised — sophisticated ransomware actors target backups first
- Recovery validation is part of your post-incident role — confirm systems are restored to a known-clean state

> 📌 **SOC Note:** Ransomware groups increasingly target backup infrastructure before deploying ransomware — they know clean backups are their greatest enemy. Watch for: unusual access to backup servers, backup agents being stopped/disabled, backup jobs failing, or non-admin accounts accessing backup software. These are early warning signs of ransomware pre-deployment activity.

---

### Control 12: Network Infrastructure Management

**What it is:** Establish, implement, and actively manage network devices to prevent attackers from exploiting vulnerable network services and access points.

**Why it matters:** Your network infrastructure (routers, switches, firewalls, VPNs) is the foundation of your environment. Compromised network devices give attackers visibility into all traffic and control over connectivity.

**Key safeguards:**
- Apply CIS Benchmarks to all network devices
- Change default credentials on all network devices immediately
- Disable unused ports, protocols, and services
- Use encrypted management protocols (SSH, not Telnet; HTTPS, not HTTP)
- Implement network segmentation — separate production from corporate, IoT from everything, OT from IT
- Regularly audit network device configurations

**SOC Analyst Role:**
- Network flow data (NetFlow/IPFIX) is a core log source for detecting lateral movement, C2 beaconing, and data exfiltration
- Segment your SIEM monitoring by network zone — a workstation communicating with OT systems is anomalous by definition
- Changes to firewall rules or network device configurations outside of approved change windows are a red flag

> 📌 **SOC Note:** Ask yourself: if a workstation is compromised, can the attacker reach your domain controllers? Your databases? Your backup servers? Good network segmentation means the answer is "no" — or at least "not without triggering alerts." If the answer is "yes, freely," escalate the segmentation gap to the GRC team as a high risk.

---

### Control 13: Network Monitoring and Defense

**What it is:** Operate processes and tooling to establish and maintain comprehensive network monitoring and defense against security threats across the environment.

**Why it matters:** Endpoint monitoring alone misses attacker activity that occurs at the network layer — lateral movement, C2 communication, data exfiltration. Network visibility fills these gaps.

**Key safeguards:**
- Deploy Network Detection and Response (NDR) / IDS / IPS solutions
- Centralize network logs to SIEM (firewall, DNS, proxy, flow data)
- Monitor for anomalous network traffic patterns
- Deploy deception technologies (honeypots, honeytokens) to catch attackers moving laterally
- Block traffic to known-malicious IPs and domains using threat intelligence feeds
- Monitor for traffic on non-standard ports or using unusual protocols

**SOC Analyst Role:**
- Network-based alerts (IDS signatures, unusual outbound traffic, DNS anomalies) form a major portion of SOC detection work
- Build network baselines — know what "normal" traffic looks like so anomalies stand out
- DNS is gold for C2 detection: DGA patterns, regular beaconing intervals, DNS tunneling all appear in DNS logs

> 📌 **SOC Note:** Every organization should be logging and analyzing DNS queries. DNS is used by malware for C2, data exfiltration (DNS tunneling), and initial infection (malicious domain resolution). If you're not watching DNS, you have a major blind spot. Tools for DNS analysis: Zeek (Bro), Suricata, Darktrace, Vectra AI, Pi-hole (for threat intel blocking).

---

### Control 14: Security Awareness and Skills Training

**What it is:** Establish and maintain a security awareness program to influence behavior, reduce human-introduced risk, and build a security culture across the organization.

**Why it matters:** The human is the most exploited attack vector. Phishing, social engineering, and insider threats all exploit human behavior. No technical control can fully compensate for a user who clicks a malicious link or is manipulated by a social engineer.

**Key safeguards:**
- Conduct regular security awareness training for all staff (minimum annually; monthly is better)
- Run phishing simulation exercises with tracked results
- Provide role-specific training (developers on secure coding, privileged users on risks, executives on targeted attacks)
- Track training completion and phishing simulation click rates as KPIs
- Create a culture where reporting suspicious activity is rewarded, never penalized

**SOC Analyst Role:**
- Effective awareness training directly reduces the volume of phishing incidents you handle
- Phishing simulation data reveals which departments and user types are most vulnerable — this feeds risk management decisions
- A "Report Phishing" button empowers users to become your human detection sensors

> 📌 **SOC Note:** A user who calls to report a suspicious email is your ally — treat them like a threat intelligence source. They may have caught something your technical controls missed. Always follow up with users who report suspicious activity so they know their report mattered. Users who feel valued become your best security sensors.

---

### Control 15: Service Provider Management

**What it is:** Develop a process to evaluate service providers who hold sensitive data or have access to your critical IT systems and processes.

**Why it matters:** Supply chain attacks are increasing dramatically. Your security is only as strong as the weakest link in your vendor ecosystem. SolarWinds, Kaseya, MOVEit, and the Target breach all involved compromised service providers.

**Key safeguards:**
- Maintain an inventory of all service providers with system access
- Classify providers by risk level (access to sensitive data, critical systems access)
- Conduct security assessments of high-risk providers (questionnaires, audits, SOC 2 report review)
- Include security requirements in all vendor contracts
- Monitor service provider access using PAM/privileged access logging
- Review and remove provider access when the engagement ends

**SOC Analyst Role:**
- Third-party and vendor access monitoring is a SOC responsibility — watch for unusual activity from service provider accounts
- Supply chain incidents often start with a trusted vendor's tools or update mechanism being weaponized — apply extra scrutiny to vendor-signed software and updates
- During incidents, always determine: "Was a vendor involved in this attack chain?"

> 📌 **SOC Note:** The Target breach (2013) — 40 million credit cards stolen — began with stolen credentials from their HVAC vendor. Always ask during an investigation: which service providers have network access, VPN accounts, or remote sessions to affected systems? Vendor access is one of the most undermonitored attack surfaces in most organizations.

---

### Control 16: Application Software Security

**What it is:** Manage the security lifecycle of developed, hosted, or acquired software to prevent, detect, and remediate weaknesses before they can be exploited.

**Why it matters:** Vulnerabilities in your own or third-party applications create direct attack paths. Web application attacks (SQL injection, XSS, authentication bypass, insecure APIs) are among the most common attack vectors.

**Key safeguards:**
- Integrate security requirements into software development from the start (Secure SDLC)
- Use Static Application Security Testing (SAST) in CI/CD pipelines
- Conduct Dynamic Application Security Testing (DAST) on running applications
- Perform Software Composition Analysis (SCA) to check third-party library vulnerabilities
- Conduct application penetration testing
- Deploy a Web Application Firewall (WAF) as a defense layer

**SOC Analyst Role:**
- WAF alerts are a direct SOC detection source — SQL injection attempts, XSS, path traversal, scanner fingerprinting
- Application logs (authentication attempts, error rates, unusual API call patterns) should feed your SIEM
- During application security incidents, collaborate with developers — they know the application logic, you know the attack patterns

> 📌 **SOC Note:** Web application attacks often start with slow reconnaissance — low-volume 404 errors, scanner fingerprinting, option enumeration. Tune your WAF and SIEM to detect the reconnaissance phase, not just successful exploitation. By the time exploitation succeeds, you've already missed multiple earlier detection opportunities.

---

### ORGANIZATIONAL CONTROLS

---

### Control 17: Incident Response Management

**What it is:** Establish a program to prepare for, detect, contain, analyze, eradicate, recover from, and communicate about security incidents.

**Why it matters:** Incidents WILL happen. The difference between a minor event and a catastrophic breach is often how fast and how effectively you respond. Without an IR program, response is chaotic, evidence is lost, and damage multiplies.

**The IR Lifecycle:**

```
PREPARE → IDENTIFY → CONTAIN → ERADICATE → RECOVER → LESSONS LEARNED
```

| Phase | Description | SOC Role |
|-------|-------------|----------|
| **Prepare** | Build playbooks, train team, set up tools, define roles | Know playbooks, tool access, escalation paths |
| **Identify** | Detect and confirm the incident | Triage alerts, determine scope, confirm severity |
| **Contain** | Limit damage — stop the spread | Isolate systems, block IPs/hashes, disable accounts |
| **Eradicate** | Remove the threat entirely | Clean systems, remove backdoors, patch vulnerabilities |
| **Recover** | Restore systems and operations | Validate clean state, restore from backup, monitor |
| **Lessons Learned** | Analyze and improve | Contribute to post-incident review, update playbooks |

**Key safeguards:**
- Develop and maintain IR playbooks for each major incident type
- Define incident severity levels and escalation paths clearly
- Conduct tabletop exercises at least annually
- Retain an IR retainer (external IR firm on contract for major incidents)
- Document all breach notification requirements (GDPR: 72 hours, HIPAA: 60 days, PCI: immediate)

> 📌 **SOC Note:** Playbooks are the most important GRC artifact for your daily work. Every major incident type should have a written playbook: ransomware, phishing, account compromise, data exfiltration, insider threat, DDoS. When a P1 fires at 2 AM, you do NOT want to be figuring out what to do. You follow the playbook. A good playbook is tested in tabletop exercises — not just documented and forgotten.

---

### Control 18: Penetration Testing

**What it is:** Test the effectiveness of your security controls through planned, authorized simulated attacks against your environment.

**Why it matters:** You cannot fully trust that controls are working until someone has tried to break them under realistic conditions. Pentest findings reveal gaps that compliance checklists and vulnerability scanners miss — especially logic flaws and attack chain combinations.

**Types of penetration testing:**

| Type | Scope | Recommended Frequency |
|------|-------|----------------------|
| **External Pentest** | Internet-facing systems | Annually minimum |
| **Internal Pentest** | Internal network, lateral movement, AD attacks | Annually minimum |
| **Web Application Pentest** | Specific web applications | Per major release + annually |
| **Red Team Exercise** | Full adversary simulation including physical and social | Every 2 years |
| **Purple Team** | Collaborative red/blue team testing specific attack chains | Quarterly for mature orgs |

**SOC Analyst Role:**
- SOC analysts are the defenders in red team and purple team exercises
- Pentests reveal detection gaps — where did the red team move without triggering an alert? Those are your blind spots
- Use pentest findings as input to build new detection rules and tune existing ones
- Purple team exercises teach you attacker techniques from MITRE ATT&CK firsthand

> 📌 **SOC Note:** After every pentest or red team exercise, go through the full report and for every technique the red team used where you did NOT detect them: **build a detection rule.** Penetration testing is the highest-quality input for improving your SIEM detection coverage. It directly answers the question: "Where are our blind spots?"

---

## 6. CIS Implementation Groups (IG1, IG2, IG3)

CIS Controls v8 introduces **Implementation Groups** to help organizations of different sizes and maturity know where to start.

| Group | Target Organization | Safeguards | Focus |
|-------|---------------------|------------|-------|
| **IG1** | Small, low-resource | 56 safeguards | Essential hygiene — the absolute minimum |
| **IG2** | Mid-size with dedicated security staff | +74 safeguards | Sensitive data protection + formal processes |
| **IG3** | Large / high-value targets | +23 safeguards | Advanced threats, sophisticated adversaries |

### IG1 — Essential Cyber Hygiene

IG1 is the **minimum baseline** for any organization. It would prevent the majority of common attacks targeting small organizations. IG1 covers the basics across all 18 controls, with emphasis on:

- Know your assets (Controls 1 & 2)
- Protect data (Control 3)
- Manage accounts and access (Controls 5 & 6)
- Maintain and monitor logs (Control 8)
- Train your people (Control 14)
- Have an incident response plan (Control 17)

### IG2 — For Organizations with Sensitive Data

Builds on IG1 with more rigorous controls:
- Formal vulnerability management programs
- Incident response planning and testing
- Network segmentation and monitoring
- Service provider management
- More rigorous configuration management

### IG3 — For High-Value Targets

Adds controls for organizations facing sophisticated, targeted attacks:
- Penetration testing programs
- Advanced threat hunting
- Application security programs
- Full network traffic analysis and NDR

### Choosing Your Starting Point

```
Organization Profile:
  Small, minimal IT staff, no dedicated security  →  Target IG1
  Mid-size, dedicated IT, some security function  →  Target IG2
  Enterprise, regulated industry, sophisticated   →  Target IG3
  threats (financial, government, healthcare)
```

---

## 7. How a SOC Analyst Works Within GRC & CIS

### The SOC in the GRC Ecosystem

```
┌─────────────────────────────────────────────────────────────────┐
│                       GRC ECOSYSTEM                              │
│                                                                   │
│   GOVERNANCE              RISK              COMPLIANCE           │
│   ───────────             ──────            ──────────          │
│   Policies                Risk Register     Audit Evidence       │
│   Procedures              Risk Appetite     Compliance Reports   │
│   Playbooks               Threat Intel      Regulatory Alerts    │
│        ↕                       ↕                  ↕             │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                    SOC ANALYST                           │    │
│  │  ▸ Monitors, detects, and responds to incidents          │    │
│  │  ▸ Generates compliance evidence (logs, tickets)         │    │
│  │  ▸ Feeds incident data into the risk register            │    │
│  │  ▸ Enforces governance controls operationally            │    │
│  │  ▸ Validates that security controls are working          │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                   │
│          CIS Controls = The HOW behind the GRC WHAT              │
└─────────────────────────────────────────────────────────────────┘
```

### Daily SOC Tasks Mapped to CIS Controls

| SOC Task | CIS Controls |
|----------|-------------|
| Triaging SIEM alerts | Control 8 (Log Management), Control 13 (Network Monitoring) |
| Investigating malware alerts | Control 10 (Malware Defenses) |
| Phishing investigation | Control 9 (Email & Web Browser) |
| Account compromise investigation | Controls 5 & 6 (Account & Access Management) |
| Lateral movement detection | Controls 12 & 13 (Network Management & Monitoring) |
| Vulnerability alert triage | Control 7 (Vulnerability Management) |
| Incident response | Control 17 (Incident Response Management) |
| Threat hunting | Controls 13 & 18 (Network Monitoring & Pentest) |
| Evidence collection for audit | Control 8 (Audit Log Management) |
| Vendor access monitoring | Control 15 (Service Provider Management) |
| WAF alert investigation | Control 16 (Application Security) |

### SOC-Specific GRC Responsibilities

**Generating Compliance Evidence**
Your SIEM reports, incident tickets, and log exports are compliance evidence. When auditors ask "can you show us your monitoring is working?" — your SOC metrics and alert data are the answer.

**Supporting Risk Assessments**
Your incident data is real-world evidence of threats materializing. Feed incident trends to the GRC team to update the risk register with actual observed threat activity rather than theoretical assumptions.

**Policy Exception Monitoring**
If a governance policy prohibits USB usage, the SOC monitors for USB insertion events and enforces the policy technically through detection and response — turning written policy into operational reality.

**Control Effectiveness Measurement**
Are your controls working? MTTD, MTTR, false positive rate, and detection coverage are your answers. This data feeds the GRC program's control assessment and drives investment decisions.

---

## 8. GRC Frameworks: The Bigger Picture

### NIST Cybersecurity Framework (CSF) 2.0

**Six Functions:**

| Function | Description | SOC Relevance |
|----------|-------------|---------------|
| **Govern** | Establish cybersecurity risk strategy and policies | Framework you operate within |
| **Identify** | Know your assets, risks, and environment | Asset inventory, threat intel |
| **Protect** | Implement safeguards to limit impact | Controls you verify are working |
| **Detect** | Identify cybersecurity events | **Core SOC function** |
| **Respond** | Take action on detected incidents | **Core SOC function** |
| **Recover** | Restore capabilities after an incident | Post-incident recovery support |

The SOC primarily operates in **Detect** and **Respond** but provides data that informs all six functions.

### ISO/IEC 27001

An internationally recognized standard for **Information Security Management Systems (ISMS)**. Organizations can achieve formal certification.

Key SOC connections:
- Annex A controls cover log monitoring, incident management, and vulnerability management
- SOC activities provide evidence for many Annex A controls during certification audits
- ISO 27001 requires a formal ISMS — GRC is the implementation vehicle

### MITRE ATT&CK Framework

While not a GRC framework, ATT&CK is the adversary behavior taxonomy that connects SOC work to CIS Controls:

- Each CIS Control defends against specific ATT&CK techniques
- SIEM detections can be mapped to ATT&CK tactics and techniques
- ATT&CK coverage measurement shows which detection gaps exist

```
Example mapping:
CIS Control 8 (Logging) enables detection of:
  T1078  — Valid Accounts (credential abuse)
  T1021  — Remote Services (lateral movement)
  T1562  — Impair Defenses (disabling security tools)
  T1070  — Indicator Removal (log clearing)
```

---

## 9. Risk Management — The Heart of GRC

### The Risk Assessment Process

**Step 1: Asset Identification**
List all assets — systems, data, processes, people — and assign business value and criticality ratings.

**Step 2: Threat Identification**
What could threaten each asset? Consider: external attackers (nation-state, cybercriminal, hacktivist), insider threats (malicious and accidental), natural disasters, supply chain compromise, and system failures.

**Step 3: Vulnerability Identification**
What weaknesses exist that threats could exploit? Unpatched software, weak access controls, misconfigured systems, untrained users, inadequate backup procedures.

**Step 4: Risk Analysis**

```
Risk Scoring Matrix:

Likelihood × Impact = Risk Score

Likelihood:
  1 = Rare | 2 = Unlikely | 3 = Possible | 4 = Likely | 5 = Almost Certain

Impact:
  1 = Negligible | 2 = Minor | 3 = Moderate | 4 = Major | 5 = Catastrophic

Risk Score:
  1–4  = Low
  5–9  = Medium
  10–16 = High
  17–25 = Critical
```

**Step 5: Risk Treatment**
For each risk: Mitigate, Accept, Transfer, or Avoid.

**Step 6: Risk Monitoring**
Risks evolve — new threats emerge, vulnerabilities are disclosed, and the business changes. Review the risk register at minimum quarterly.

### SOC's Contribution to Risk Management

| SOC Activity | Risk Management Value |
|-------------|----------------------|
| Incident detection and investigation | Confirms threats are real and active — updates likelihood ratings |
| Threat intelligence consumption | Identifies emerging threats relevant to your environment |
| Penetration test support | Reveals real-world exploitability — updates impact ratings |
| Vulnerability scan data analysis | Quantifies attack surface and control gaps |
| SIEM detection metrics | Measures control effectiveness objectively |

---

## 10. Compliance Mapping — CIS to Other Frameworks

Implementing CIS Controls simultaneously satisfies requirements across multiple compliance frameworks — significant efficiency.

### CIS Controls Compliance Mapping Table

| CIS Control | PCI DSS v4 | HIPAA Security Rule | ISO 27001:2022 | NIST CSF 2.0 |
|-------------|------------|---------------------|----------------|--------------|
| 1 — Asset Inventory | Req 12.5 | §164.310(d) | A.8.1 | ID.AM |
| 2 — Software Inventory | Req 6.3 | §164.312(a) | A.8.1 | ID.AM |
| 3 — Data Protection | Req 3, 4 | §164.312(e) | A.8.2, A.8.3 | PR.DS |
| 4 — Secure Config | Req 2.2, 6.3 | §164.312(a)(2)(iv) | A.8.9 | PR.IP |
| 5 — Account Mgmt | Req 7, 8 | §164.312(a)(2) | A.5.15, A.5.16 | PR.AC |
| 6 — Access Control | Req 7, 8 | §164.312(a)(2) | A.5.15, A.9.2 | PR.AC |
| 7 — Vulnerability Mgmt | Req 6, 11 | §164.308(a)(8) | A.8.8 | ID.RA |
| 8 — Audit Logs | Req 10 | §164.312(b) | A.8.15, A.8.17 | DE.CM |
| 9 — Email/Web | Req 6.3 | §164.308(a)(5) | A.8.23 | PR.AT, DE.CM |
| 10 — Malware | Req 5 | §164.308(a)(5) | A.8.7 | DE.CM |
| 13 — Network Monitoring | Req 10, 11 | §164.308(a)(1) | A.8.16 | DE.CM |
| 17 — Incident Response | Req 12.10 | §164.308(a)(6) | A.5.24, A.5.26 | RS |
| 18 — Penetration Testing | Req 11.4 | §164.308(a)(8) | A.8.8 | ID.RA |

### The Efficiency Argument for Leadership

> "By implementing CIS Controls IG2, we simultaneously satisfy 80%+ of our PCI DSS requirements, address HIPAA Security Rule safeguards, and align with ISO 27001 Annex A controls — with a single coordinated program rather than three separate compliance efforts."

---

## 11. GRC Tools a SOC Analyst Should Know

### GRC Platforms

| Tool | Description |
|------|-------------|
| **ServiceNow GRC** | Enterprise GRC — policy management, risk assessments, compliance tracking |
| **RSA Archer** | Risk management, compliance, and audit management |
| **OneTrust** | Privacy, compliance, and risk management |
| **Vanta / Drata / Secureframe** | Automated continuous compliance for cloud-native organizations |
| **LogicGate** | GRC workflow automation |

### Security Tools That Support CIS Controls

| Tool | CIS Controls Supported |
|------|----------------------|
| **Tenable / Qualys** | Controls 1, 2, 7 (Asset and vulnerability management) |
| **CrowdStrike / SentinelOne (EDR)** | Controls 4, 10 (Secure config validation, malware defenses) |
| **Splunk / Microsoft Sentinel (SIEM)** | Controls 8, 13 (Log management, network monitoring) |
| **Palo Alto / Fortinet (Firewall/NGFW)** | Controls 9, 12, 13 (Network protection and monitoring) |
| **CyberArk / BeyondTrust (PAM)** | Controls 5, 6 (Account and access management) |
| **KnowBe4 / Proofpoint (Awareness)** | Control 14 (Security awareness training) |
| **Zeek / Suricata (NDR/IDS)** | Control 13 (Network detection) |
| **CIS-CAT Tool** | Control 4 (Automated CIS Benchmark assessment) |

### Free CIS Resources

- **CIS Benchmarks** — Free secure configuration guides for 100+ technologies
- **CIS-CAT Lite** — Free automated configuration assessment tool
- **CIS Controls Assessment Tool (CCAT)** — Free self-assessment of CIS Controls implementation
- All available at: `https://www.cisecurity.org`

---

## 12. SOC Analyst Daily Touchpoints with GRC

### Start-of-Shift Routine Mapped to GRC & CIS

```
Start of Shift:
  1. Review overnight SIEM alerts              → CIS Control 8 & 13
  2. Check vulnerability scanner for new       → CIS Control 7
     critical/high findings
  3. Review threat intelligence feed           → Risk Management + Control 13
  4. Verify all log sources are healthy        → CIS Control 8
     (flag any unexpected silence)
  5. Check change management for overnight     → Governance (Change Mgmt Policy)
     approved changes (distinguish from noise)
```

### Incident Response Flow Mapped to GRC

```
P1 Incident Fires:
  1. Classify severity per IR Policy           → Governance (Incident Policy)
  2. Open incident ticket (start audit trail)  → Compliance (Audit Evidence)
  3. Pull affected asset from CMDB             → CIS Control 1 (Asset Inventory)
  4. Check vulnerability scan data for host    → CIS Control 7 (Vuln Mgmt)
  5. Follow the IR playbook for incident type  → Governance (Procedure)
  6. Contain per your authorization level      → Governance + CIS Control 17
  7. Document every action taken               → Compliance (Evidence Chain)
  8. Notify per breach notification policy     → Compliance (Regulatory)
  9. Post-incident: update risk register       → Risk Management
  10. Participate in lessons learned           → CIS Control 17
```

### Evidence You Generate Daily for Compliance

| Your Activity | Compliance Evidence Produced |
|---------------|------------------------------|
| SIEM alert triage | Proof of continuous security monitoring |
| Incident ticket documentation | Incident response records |
| Vulnerability report review | Vulnerability management program evidence |
| Log source health monitoring | Audit log integrity and availability evidence |
| Threat intel consumption and action | Threat awareness and proactive defense documentation |

---

## 13. Metrics & Reporting for SOC Within GRC

### Core SOC Metrics

**Detection & Response:**

| Metric | Description | Target |
|--------|-------------|--------|
| **MTTD** | Mean Time to Detect — compromise to detection | < 24 hours |
| **MTTR** | Mean Time to Respond — detection to containment | < 4 hours (P1) |
| **False Positive Rate** | % of alerts that are not real incidents | < 10% (well-tuned SIEM) |
| **Alert Volume Trend** | Total alerts per period — trending up or down | Track trend |
| **Incidents by Severity** | Count of P1/P2/P3/P4 per period | Track trend |

**Coverage:**

| Metric | Description | Target |
|--------|-------------|--------|
| **Log Source Coverage** | % of expected sources actively sending logs | 100% |
| **MITRE ATT&CK Coverage** | % of techniques with at least one detection | Improve quarterly |
| **Asset Monitoring Coverage** | % of assets with logging/monitoring enabled | 100% |
| **CIS Control Implementation Rate** | % of IG-applicable safeguards implemented | Track progress |

### Executive Dashboard (Business Language)

Non-technical leadership needs security metrics in business terms:
- **Risk Posture Trend** — Improving / Stable / Degrading
- **Critical Incidents This Month** — Count with trend direction
- **Time to Detect & Respond** — Trending in the right direction?
- **Patch Compliance Rate** — % of critical vulns patched within SLA
- **Compliance Status** — Red/Amber/Green by framework
- **Top 5 Risks** — Current highest risks with treatment status

---

## 14. Building & Maturing a GRC Program

### The Security Maturity Model

| Level | Name | Description |
|-------|------|-------------|
| **1** | Initial | Ad-hoc, reactive, no formal processes |
| **2** | Developing | Some processes documented, inconsistently applied |
| **3** | Defined | Documented, standardized, consistently followed |
| **4** | Managed | Measured, metrics-driven, proactive |
| **5** | Optimizing | Continuous improvement, benchmarked against peers |

Most organizations start at Level 1–2. The realistic goal for most organizations is Level 3–4.

### CIS Controls Quick-Start Roadmap

**Months 1–3: IG1 Foundation**
- [ ] Complete hardware asset inventory (Control 1)
- [ ] Complete software asset inventory (Control 2)
- [ ] Implement MFA on all accounts (Control 6)
- [ ] Enable logging on all key systems, feed to SIEM (Control 8)
- [ ] Deploy EDR on all endpoints (Control 10)
- [ ] Conduct basic security awareness training (Control 14)
- [ ] Write Incident Response Policy and at least one playbook (Control 17)

**Months 4–6: IG1 Completion + IG2 Start**
- [ ] Deploy weekly vulnerability scanning (Control 7)
- [ ] Establish patch remediation SLAs and track compliance (Control 7)
- [ ] Implement secure configuration baselines via CIS Benchmarks (Control 4)
- [ ] Deploy email security: anti-phishing + DMARC/DKIM/SPF (Control 9)
- [ ] Begin basic network segmentation (Control 12)
- [ ] Build initial SIEM detection rules (Controls 8, 13)

**Months 7–12: IG2 Progress**
- [ ] Conduct formal risk assessment and establish risk register (Risk Mgmt)
- [ ] Conduct first tabletop exercise (Control 17)
- [ ] Implement DLP for sensitive data (Control 3)
- [ ] Establish vendor risk management process (Control 15)
- [ ] Conduct first penetration test (Control 18)
- [ ] Implement GRC tool for policy and risk tracking

---

## 15. Common GRC Mistakes and How to Avoid Them

### Mistake 1: Treating GRC as Pure Compliance Theater

**Problem:** Checking boxes to pass an audit without actually improving security.

**Fix:** CIS Controls are your antidote — they're derived from actual attack data, not regulator checklists. Use them alongside compliance frameworks to build real security, not just paper security.

---

### Mistake 2: No Asset Inventory (or a Stale One)

**Problem:** You cannot govern, risk-manage, or secure what you don't know exists.

**Fix:** CIS Control 1 is first for a reason. Asset inventory is the foundation. Invest in continuous discovery tooling and maintain the inventory actively — a one-time snapshot becomes useless within months.

---

### Mistake 3: GRC Lives Only in Documents

**Problem:** Beautiful policies and risk registers that no one reads or follows.

**Fix:** GRC must be operationalized. SOC processes must reflect policies. Controls must be technically enforced, not just documented. If the policy says "log all privileged access" but your SIEM isn't receiving those logs, the policy is theater.

---

### Mistake 4: GRC and SOC Work in Isolation

**Problem:** GRC sets requirements the SOC doesn't know about. SOC incident findings don't reach the risk register.

**Fix:** Establish regular communication bridges. SOC should attend risk review meetings. GRC should review major incident reports. The SOC's real-world threat data is the GRC program's most valuable input.

---

### Mistake 5: Ignoring Third-Party Risk

**Problem:** Strong internal controls, but vendors with access to your environment have weak security.

**Fix:** CIS Control 15. Every vendor with system access needs a security assessment. Every vendor agreement needs security requirements. Monitor vendor access like you monitor employee access — with the same scrutiny.

---

### Mistake 6: Risk Acceptance Without Documentation

**Problem:** Someone verbally accepts a risk. When an incident occurs from that risk, there's no record.

**Fix:** Every risk acceptance must be a formal, written, signed document containing: the risk description, the business justification for acceptance, compensating controls in place, the risk owner, and a mandatory review date.

---

## 16. SOC Analyst Notes & Quick Reference

> *Practical field notes for day-to-day SOC work within a GRC framework.*

---

### Note 1: Know Your Policies Before You Need Them

Read your key policies before an incident. Know:
- What constitutes a "reportable breach" under your policy?
- Who do you call for a P1 at 3 AM?
- What is your authority to isolate a system without pre-approval?
- What is your log retention period?

You will not have time to look these up during an active incident.

---

### Note 2: The Asset Inventory Is Your First Stop During IR

When an alert fires, immediately look up the affected asset in the CMDB:
- What is this system?
- What data does it hold (data classification)?
- Who is the business owner?
- What is its criticality rating?
- What does it connect to?

Without this context, your severity assessment is guesswork.

---

### Note 3: Log Source Silence Is an Alert

A log source going silent means one of two things:
1. A technical problem (agent failure, network disruption)
2. An attacker disabled or tampered with logging

**Both are actionable.** Build an alert: "Log source X has not sent events in N hours." This is basic but powerful — and gives you early warning of either operational issues or attacker anti-forensics.

---

### Note 4: Map Every Detection Rule to CIS Controls and ATT&CK

For every SIEM rule, document:
- Which MITRE ATT&CK technique it detects (e.g., T1059 — Command and Scripting Interpreter)
- Which CIS Control it validates (e.g., Control 10 — Malware Defenses)

This turns your SIEM rule library into GRC compliance evidence — proof that controls are implemented and operationally active.

---

### Note 5: False Positive Rate Is a GRC Risk

A SIEM with 90% false positives drowns analysts in noise, causing real incidents to be missed. This is a documented risk — it increases MTTD. Quantify it, report it, and escalate it to the GRC team as a control effectiveness issue that requires investment to fix.

---

### Note 6: Breach Notification Timelines Are Hard Deadlines

Know your regulatory notification windows cold:

| Regulation | Required Notification Window |
|------------|------------------------------|
| **GDPR** | 72 hours to supervisory authority |
| **HIPAA** | 60 days to HHS; media notification if >500 affected |
| **PCI DSS** | Immediately to card brands and acquiring bank |
| **CCPA** | "Without unreasonable delay" |
| **NY SHIELD Act** | "In the most expedient time possible" |

When a P1 incident looks like a breach, escalate early. Legal and compliance need time to evaluate notification requirements — give them that time.

---

### Note 7: CIS Controls Priority Order for SOC

```
When asked "where do we start?" — use this priority order:

IMMEDIATELY:
  ✅ Asset Inventory (Control 1)
  ✅ MFA on All Accounts (Control 6)
  ✅ EDR on All Endpoints (Control 10)
  ✅ Log Everything to SIEM (Control 8)
  ✅ IR Playbooks Written and Tested (Control 17)

THIS QUARTER:
  ✅ Weekly Vulnerability Scanning (Control 7)
  ✅ Secure Configuration Baselines (Control 4)
  ✅ Email Security + DMARC (Control 9)
  ✅ Security Awareness Training (Control 14)
  ✅ Account Lifecycle Management (Control 5)

OVER 6 MONTHS:
  ✅ Network Segmentation (Control 12)
  ✅ Network Detection/NDR (Control 13)
  ✅ DLP Implementation (Control 3)
  ✅ Vendor Risk Management (Control 15)
  ✅ Penetration Testing (Control 18)
```

---

### Note 8: Incident Type → CIS Control Quick Reference

```
Incident Type            →  Primary CIS Controls to Reference
──────────────────────────────────────────────────────────────
Phishing                 →  9 (Email), 14 (Awareness)
Malware / Ransomware     →  2, 4, 10, 11
Account Compromise       →  5, 6
Privilege Escalation     →  5, 6
Lateral Movement         →  12, 13
Data Exfiltration        →  3, 9, 13
Insider Threat           →  5, 6, 8
Supply Chain Attack      →  15, 16
Unpatched Exploit        →  7
Unauthorized Config Chg  →  4, 8
Unknown Device on Network →  1, 12
Log Tampering / Clearing →  8
Web Application Attack   →  16
```

---

### Note 9: The SOC Analyst's GRC Mindset

Shift your thinking:

| Old Mindset | GRC Mindset |
|-------------|-------------|
| "I respond to alerts" | "I operationally enforce the organization's security controls and generate evidence of their effectiveness" |
| "GRC is the compliance team's problem" | "My incident data is the GRC team's most valuable real-world input" |
| "Compliance is checkbox work" | "Compliance is the floor; CIS Controls help us build real security above it" |
| "That alert isn't my problem" | "Every alert is evidence of a control working or failing — both matter" |

---

### Note 10: Key Windows Event IDs for GRC-Aligned Investigations

```
Account Management:
  4720  Account Created
  4722  Account Enabled
  4725  Account Disabled
  4726  Account Deleted
  4728  Member Added to Security-Enabled Global Group
  4732  Member Added to Security-Enabled Local Group
  4740  Account Locked Out

Authentication:
  4624  Successful Logon
  4625  Failed Logon
  4648  Logon with Explicit Credentials (Pass-the-Hash indicator)
  4672  Special Privileges Assigned to New Logon (Admin logon)
  4768  Kerberos TGT Request
  4769  Kerberos Service Ticket Request

System Integrity:
  1102  Security Audit Log Cleared  ← P1 Alert
  104   System Log Cleared          ← P1 Alert
  7045  New Service Installed       ← Persistence indicator
  4698  Scheduled Task Created      ← Persistence indicator

Process & Execution (via Sysmon):
  1     Process Creation
  3     Network Connection
  11    File Created
  13    Registry Value Set
```

---

## 17. Glossary

| Term | Definition |
|------|------------|
| **APT** | Advanced Persistent Threat — sophisticated, long-duration, often nation-state adversary |
| **Asset** | Any hardware, software, data, or person of value to the organization |
| **Audit** | Independent examination of controls, evidence, and processes |
| **Benchmark** | CIS-published secure configuration guide for a specific technology |
| **CISO** | Chief Information Security Officer — top security executive |
| **CIS** | Center for Internet Security — nonprofit that publishes CIS Controls and Benchmarks |
| **CMDB** | Configuration Management Database — authoritative IT asset inventory |
| **Compensating Control** | Alternative control used when the primary control cannot be implemented |
| **Compliance** | Adherence to laws, regulations, standards, or contractual obligations |
| **Control** | A safeguard or countermeasure designed to reduce risk |
| **CVSS** | Common Vulnerability Scoring System — standardized severity rating for vulnerabilities |
| **DLP** | Data Loss Prevention — tools and policies to prevent unauthorized data transfer |
| **EDR** | Endpoint Detection and Response — advanced behavioral endpoint security platform |
| **GRC** | Governance, Risk, and Compliance |
| **IG1/IG2/IG3** | CIS Implementation Groups — tiered implementation levels based on org maturity |
| **Incident** | A security event that compromises or threatens to compromise confidentiality, integrity, or availability |
| **IOC** | Indicator of Compromise — evidence of an attack (IP address, file hash, domain) |
| **IR** | Incident Response |
| **ISMS** | Information Security Management System — the formal management framework in ISO 27001 |
| **Least Privilege** | Users and systems have only the minimum access needed for their function |
| **MTTD** | Mean Time to Detect — average time from compromise to detection |
| **MTTR** | Mean Time to Respond — average time from detection to containment |
| **MITRE ATT&CK** | Knowledge base of adversary tactics, techniques, and procedures (TTPs) |
| **NDR** | Network Detection and Response |
| **PAM** | Privileged Access Management — tools to control and monitor administrative access |
| **Policy** | High-level statement of management's security intent and direction |
| **Procedure** | Step-by-step operational instructions for performing a task |
| **RBAC** | Role-Based Access Control — access permissions assigned based on job role |
| **Risk** | The potential for harm — function of threat, vulnerability, and impact |
| **Risk Register** | Documented list of identified risks with assessment, treatment, and ownership |
| **SIEM** | Security Information and Event Management — centralized log analysis and alerting platform |
| **SOC** | Security Operations Center |
| **Standard** | Mandatory technical specifications that support a security policy |
| **TTP** | Tactics, Techniques, and Procedures — how adversaries operate |
| **Vulnerability** | A weakness in a system that could be exploited by a threat |
| **WAF** | Web Application Firewall — protects web applications from common attacks |
| **Zero-Day** | A vulnerability with no available vendor patch |

---

## Summary

GRC and CIS Controls form the complete operating framework for a mature, defensible security organization:

- **GRC** provides the *why* and *what* — the policies, risk decisions, and compliance obligations that define what security the organization must have and the business reasons behind it
- **CIS Controls** provide the *how* — 18 specific, prioritized controls derived from real attack data that tell you exactly what to implement and in what order
- **The SOC** is where GRC becomes real — you are the operational arm that enforces controls, detects their failure, generates compliance evidence, and feeds real-world threat intelligence back into the risk management process

As a SOC analyst, GRC knowledge makes you dramatically more effective:

- Investigations are faster because asset context, data classification, and network documentation exist
- Escalations are better because you understand IR policy and regulatory notification timelines
- Detection coverage improves because rules are mapped to CIS Controls and MITRE ATT&CK
- Your career grows because you understand security as a business function, not just a technical discipline
- Your work is defensible because it's documented, measured, and aligned to a recognized framework

> *"The best SOC analysts don't just respond to alerts. They understand the security program they're defending, the risks their organization faces, and how their daily work contributes to a defensible, measurable security posture. That understanding comes from GRC."*

---

*Document maintained as part of the Security Knowledge Base.*
*Framework references: CIS Controls v8 | NIST CSF 2.0 | ISO/IEC 27001:2022 | MITRE ATT&CK v14 | NIST SP 800-53 Rev 5*
*Audience: SOC Analysts (Tier 1/2/3) | Security Engineers | GRC Analysts | Security Managers*
