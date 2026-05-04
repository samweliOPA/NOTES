# 🛡️ Patch Management: The Art and Science of Closing the Door on Attackers

> *"An unpatched vulnerability is an open invitation. Patch management is the discipline of revoking that invitation — systematically, continuously, and intelligently."*

---

## Table of Contents

1. [What Is Patch Management?](#1-what-is-patch-management)
2. [Why Patch Management Matters](#2-why-patch-management-matters)
3. [The Threat Landscape: Why Attackers Love Unpatched Systems](#3-the-threat-landscape-why-attackers-love-unpatched-systems)
4. [Core Concepts and Terminology](#4-core-concepts-and-terminology)
5. [Types of Patches](#5-types-of-patches)
6. [The Patch Management Lifecycle](#6-the-patch-management-lifecycle)
7. [Vulnerability Scoring and Prioritization](#7-vulnerability-scoring-and-prioritization)
8. [Patch Management Strategies](#8-patch-management-strategies)
9. [Tools and Technologies](#9-tools-and-technologies)
10. [Patch Management in Different Environments](#10-patch-management-in-different-environments)
11. [The Human Element: Culture and Process](#11-the-human-element-culture-and-process)
12. [Metrics and KPIs](#12-metrics-and-kpis)
13. [Common Challenges and How to Overcome Them](#13-common-challenges-and-how-to-overcome-them)
14. [Compliance and Regulatory Requirements](#14-compliance-and-regulatory-requirements)
15. [Zero-Day Vulnerabilities: When There Is No Patch](#15-zero-day-vulnerabilities-when-there-is-no-patch)
16. [Patch Management Best Practices](#16-patch-management-best-practices)
17. [Building a Patch Management Policy](#17-building-a-patch-management-policy)
18. [Glossary](#18-glossary)

---

## 1. What Is Patch Management?

**Patch management** is the systematic process of identifying, acquiring, testing, deploying, and verifying software updates (patches) across an organization's IT infrastructure. It is one of the most fundamental disciplines in cybersecurity and IT operations.

At its core, patch management answers three questions:

- **What** systems and software do we have?
- **What** vulnerabilities or bugs exist in them?
- **How** do we fix them efficiently and safely?

### The "Art" vs. The "Science"

The title of this subject — *the art and science* — is deliberate. Patch management has two dimensions:

| Dimension | Description |
|-----------|-------------|
| **Science** | Systematic processes, vulnerability scoring, automation, metrics, SLAs, tooling |
| **Art** | Judgment calls on prioritization, managing business risk, stakeholder communication, knowing when NOT to patch |

Both dimensions are essential. Pure science without art leads to rigid processes that break production. Pure art without science leads to inconsistency and gaps that attackers exploit.

---

## 2. Why Patch Management Matters

### Real-World Impact

Some of the most devastating cyberattacks in history were caused entirely by unpatched systems:

- **WannaCry (2017)** — Ransomware that infected 230,000+ computers across 150 countries. It exploited `EternalBlue`, a vulnerability in Windows SMB that Microsoft had patched **57 days earlier** in MS17-010. Organizations that had not applied the patch suffered catastrophic losses (estimated $4–8 billion globally).

- **Equifax Data Breach (2017)** — 147 million people's personal data was exposed. The root cause was an unpatched Apache Struts vulnerability (CVE-2017-5638) that had a publicly available fix **for 2 months** before the breach.

- **NotPetya (2017)** — Also exploited EternalBlue. Caused over $10 billion in damage worldwide, crippling shipping giant Maersk, pharmaceutical company Merck, and others.

> **Key insight:** The vast majority of successful attacks exploit known vulnerabilities with available patches. The adversary's job is often trivial when defenders don't patch.

### The Economics of Patching

| Cost of Patching | Cost of NOT Patching |
|-----------------|---------------------|
| Engineer time | Breach investigation and response |
| Downtime during maintenance windows | Regulatory fines |
| Testing effort | Legal liability |
| Tool licensing | Reputational damage |
| Risk of patch breaking something | Data loss/theft |
| — | Ransomware payments |
| — | Business continuity disruption |

The cost of patching is **always** less than the cost of a breach caused by an unpatched vulnerability.

---

## 3. The Threat Landscape: Why Attackers Love Unpatched Systems

### The Attacker's Perspective

From an attacker's point of view, unpatched vulnerabilities are valuable because:

- **Reliability** — Known exploits work consistently. Attackers don't have to discover new vulnerabilities; they just scan for systems that haven't applied existing fixes.
- **Speed** — Exploit code for known CVEs (Common Vulnerabilities and Exposures) is often publicly available within days of a patch release. This creates a dangerous race window.
- **Scale** — Automated scanners can identify thousands of vulnerable hosts globally in minutes.
- **Low skill barrier** — "Script kiddies" and commodity ransomware groups don't need sophisticated skills to use publicly available exploit frameworks like Metasploit.

### The Exploit Window

```
Vendor discovers vulnerability → Patch released → Patch applied by org
        [Private]                  [Public]            [Safe]
                                      ↑
                                 DANGER ZONE
                         (exploit code published here)
```

The danger zone — between patch release and patch application — is when organizations are most at risk. Attackers monitor patch releases, reverse-engineer what was fixed, and write exploits. This gap is sometimes called the **"patch gap"** or **"window of vulnerability."**

Studies show that:
- 50% of vulnerabilities are exploited within **2 weeks** of a patch release
- Critical vulnerabilities are often weaponized within **24–72 hours**

---

## 4. Core Concepts and Terminology

### CVE — Common Vulnerabilities and Exposures

A **CVE** is a standardized identifier for a publicly known security vulnerability. Maintained by MITRE and funded by the US government.

**Format:** `CVE-[YEAR]-[NUMBER]`
**Example:** `CVE-2021-44228` (Log4Shell)

Every CVE has:
- A unique ID
- A description of the vulnerability
- References to advisories and patches

### CVSS — Common Vulnerability Scoring System

**CVSS** is a framework for rating the severity of vulnerabilities. It produces a numeric score from **0.0 to 10.0**.

| Score Range | Severity |
|-------------|----------|
| 0.0 | None |
| 0.1 – 3.9 | Low |
| 4.0 – 6.9 | Medium |
| 7.0 – 8.9 | High |
| 9.0 – 10.0 | Critical |

**CVSS is based on three metric groups:**

- **Base Metrics** — Inherent characteristics (attack vector, complexity, privileges required, impact)
- **Temporal Metrics** — How the severity changes over time (exploit maturity, remediation level)
- **Environmental Metrics** — Adjusted for your specific environment

### Vulnerability vs. Exploit vs. Patch

| Term | Definition |
|------|------------|
| **Vulnerability** | A flaw or weakness in software/hardware that could be exploited |
| **Exploit** | Code or technique that takes advantage of a vulnerability |
| **Patch** | An update from the vendor that fixes the vulnerability |
| **Hotfix** | An urgent, often unscheduled patch for a critical issue |
| **Service Pack** | A large bundle of patches, fixes, and updates |

### Asset Inventory

You cannot patch what you don't know you have. An **asset inventory** is a comprehensive list of all hardware and software in the environment. This is the foundation of patch management.

---

## 5. Types of Patches

### By Purpose

| Type | Description | Example |
|------|-------------|---------|
| **Security Patch** | Fixes a vulnerability that could be exploited | MS17-010 (EternalBlue fix) |
| **Bug Fix** | Corrects non-security defects that cause errors or instability | Application crash fix |
| **Feature Update** | Adds new functionality | New UI features |
| **Driver Update** | Updates hardware drivers | GPU driver update |
| **Firmware Update** | Updates embedded software in hardware | Router firmware |

### By Urgency

- **Emergency/Out-of-Band Patch** — Released outside the normal patch cycle due to active exploitation or critical severity. Must be deployed immediately.
- **Critical Patch** — High CVSS score, requires fast-tracked deployment (typically within 24–72 hours).
- **Routine Patch** — Low-to-medium severity, applied in the regular patch cycle.

### By Scope

- **OS Patches** — Operating system level (Windows Update, RHEL errata, Ubuntu APT)
- **Application Patches** — Third-party software (Office, Browsers, Adobe, Java)
- **Middleware Patches** — Web servers, databases, application servers (Apache, Nginx, Oracle, MySQL)
- **Firmware Patches** — Network devices, IoT, BIOS/UEFI

---

## 6. The Patch Management Lifecycle

The patch management process is a continuous cycle, not a one-time event. Here is the standard lifecycle:

```
    ┌──────────────────────────────────────────────────────┐
    │                PATCH MANAGEMENT LIFECYCLE             │
    └──────────────────────────────────────────────────────┘

  ① DISCOVER          ② ASSESS           ③ PRIORITIZE
  ─────────────       ──────────────      ──────────────────
  Inventory all       Scan for            Rank by CVSS,
  assets and          vulnerabilities     exploitability,
  software            against known CVEs  asset criticality

        ↓                   ↓                    ↓

  ⑦ REPORT           ⑥ VERIFY           ④ TEST
  ─────────────       ──────────────      ──────────────────
  Track KPIs,         Confirm patch       Apply in dev/UAT,
  compliance,         applied, vuln       validate no
  audit trails        closed, systems up  breakage

        ↑                   ↑                    ↓

                      ⑤ DEPLOY
                      ──────────────────
                      Roll out in waves:
                      Dev → Test → Prod,
                      with rollback plan
```

### Step 1: Discovery and Asset Inventory

Before you can patch, you must know what you have.

- Maintain a **Configuration Management Database (CMDB)**
- Use automated discovery tools (Nessus, Qualys, Lansweeper, ServiceNow)
- Include: servers, workstations, laptops, network devices, IoT, cloud instances, containers
- Track: OS version, installed software and versions, patch status, business owner, criticality

**Common mistake:** Organizations forget about shadow IT — systems deployed without IT's knowledge. Cloud sprawl (unauthorized AWS/Azure resources) is a major source of unmanaged, unpatched assets.

### Step 2: Vulnerability Assessment and Scanning

Use vulnerability scanners to identify which assets have known vulnerabilities.

**Types of scans:**
- **Authenticated scan** — The scanner logs into the system; much more accurate
- **Unauthenticated scan** — External perspective; shows what attackers see, but less complete
- **Agent-based scan** — An agent runs on the endpoint; works even without network visibility

**Scanning frequency recommendations:**
- Critical systems: Weekly or continuous
- Production servers: Weekly
- Workstations: Monthly
- Network devices: Monthly

### Step 3: Prioritization

Not all patches are equal. You cannot patch everything instantly. Prioritization must consider:

**Risk factors:**
- CVSS score of the vulnerability
- Exploitability (is there public exploit code? Is it being exploited in the wild?)
- Criticality of the affected asset (core banking system vs. test workstation)
- Exposure (internet-facing vs. internal)
- Compensating controls (Is there a WAF or IDS that mitigates it?)

**Prioritization tiers (example SLA):**

| Tier | Criteria | Remediation SLA |
|------|----------|-----------------|
| P1 – Critical | CVSS 9+, actively exploited, internet-facing | 24 hours |
| P2 – High | CVSS 7–8.9, exploit code available | 7 days |
| P3 – Medium | CVSS 4–6.9, no public exploit | 30 days |
| P4 – Low | CVSS < 4 | 90 days |

> ⚠️ **CVSS alone is not enough.** A CVSS 9.8 vulnerability in a sandboxed test system that has no sensitive data and no internet access is less urgent than a CVSS 6.5 vulnerability on an internet-facing authentication server.

### Step 4: Testing

**Never deploy patches directly to production.** Testing catches:
- Patch conflicts with existing software
- Application breakage
- Performance regressions
- Configuration changes introduced by the patch

**Testing environments (in order):**
1. **Development (Dev)** — Initial patch application and basic functionality testing
2. **Quality Assurance (QA/UAT)** — User acceptance testing, regression testing
3. **Staging** — Production-identical environment for final validation
4. **Production** — Phased rollout after all prior stages pass

**Always have a rollback plan** — Document how to uninstall the patch or restore from backup if things go wrong.

### Step 5: Deployment

**Deployment strategies:**

- **Phased/Wave Rollout** — Deploy to small groups first, then expand. E.g., 5% → 25% → 100% of systems.
- **Maintenance Windows** — Schedule patches during low-traffic periods to minimize business impact
- **Push vs. Pull** — Push patches from a central server (WSUS, SCCM) vs. endpoints pulling updates themselves
- **Automated vs. Manual** — Automate routine patches; manually oversee critical or complex patches

**Deployment considerations:**
- Communicate maintenance windows to stakeholders in advance
- Ensure backups are current before deploying
- Have rollback/restore procedures documented and tested
- Monitor systems during and after deployment for errors

### Step 6: Verification

After deployment, confirm:
- The patch was actually applied (check patch status, not just deployment logs)
- The vulnerability is closed (re-scan to confirm)
- Systems are functioning normally (application monitoring)

**Common mistake:** Confusing "patch deployed" with "vulnerability closed." A patch can be deployed but fail to apply due to locked files, pending reboots, or conflicts.

### Step 7: Reporting and Documentation

- Maintain records of all patches applied, dates, and systems affected
- Track patch compliance rates (what % of systems are patched within SLA?)
- Report to leadership on risk posture
- Maintain audit trail for compliance purposes (PCI DSS, HIPAA, ISO 27001)

---

## 7. Vulnerability Scoring and Prioritization

### CVSS Deep Dive

The **Base Score** is calculated from:

**Exploitability Metrics:**
- **Attack Vector (AV)** — Network, Adjacent, Local, Physical (Network is highest risk)
- **Attack Complexity (AC)** — Low, High
- **Privileges Required (PR)** — None, Low, High
- **User Interaction (UI)** — None, Required

**Impact Metrics:**
- **Confidentiality Impact (C)** — None, Low, High
- **Integrity Impact (I)** — None, Low, High
- **Availability Impact (A)** — None, Low, High

**Example:** Log4Shell (CVE-2021-44228)
- Attack Vector: Network (attackers exploit it remotely)
- Attack Complexity: Low (trivial to exploit)
- Privileges Required: None
- User Interaction: None
- Confidentiality Impact: High
- Integrity Impact: High
- Availability Impact: High
- **CVSS Score: 10.0 (Maximum)**

### Beyond CVSS: EPSS

The **Exploit Prediction Scoring System (EPSS)** is a newer model that estimates the **probability** that a vulnerability will be exploited in the wild within 30 days. It ranges from 0 to 1 (0%–100%).

EPSS + CVSS together give a much better picture than CVSS alone:

| CVSS | EPSS | Priority |
|------|------|----------|
| High | High | 🔴 Immediate action |
| High | Low | 🟡 Patch this cycle |
| Low | High | 🟠 Patch soon (being exploited despite low score) |
| Low | Low | 🟢 Routine |

### Threat Intelligence Integration

The best patch prioritization also considers:
- **CISA KEV (Known Exploited Vulnerabilities)** — A US government catalog of CVEs actively exploited in the wild. These should always be treated as P1 regardless of CVSS.
- **Threat intelligence feeds** — Information on what adversary groups are actively exploiting
- **Dark web monitoring** — Are exploit kits for this vulnerability being sold?

---

## 8. Patch Management Strategies

### Reactive vs. Proactive

| Approach | Description | Risk |
|----------|-------------|------|
| **Reactive** | Patch only when an incident occurs or audit demands it | Very High — attackers exploit the gap |
| **Proactive** | Continuous, scheduled patching before vulnerabilities are exploited | Low — closes the door before attackers walk in |

Always aim for a **proactive** approach.

### Continuous Patching

Modern organizations are shifting toward continuous patching — using automation to apply patches as soon as they are released and validated, rather than waiting for monthly windows.

**Benefits:**
- Dramatically reduces the window of vulnerability
- Reduces the backlog that accumulates between cycles

**Challenges:**
- Requires robust testing automation
- Risk of patch-induced outages if testing is insufficient

### Risk-Based Patching

Rather than patching everything on the same schedule, **risk-based patching** focuses resources on the highest-risk vulnerabilities first based on:
- Asset criticality (what is the impact if this system is compromised?)
- Vulnerability severity and exploitability
- Exposure (is it internet-facing?)

This approach is more efficient and aligns security with business priorities.

### Compensating Controls

Sometimes a patch cannot be applied immediately (due to compatibility, vendor support, or business constraints). In these cases, implement **compensating controls** to reduce risk while a patch is being scheduled:

- Network segmentation / firewall rules to limit exposure
- Web Application Firewall (WAF) rules to block known exploit patterns
- Disabling affected features or services
- Enhanced monitoring for exploitation attempts
- Intrusion Detection/Prevention Systems (IDS/IPS)

Compensating controls are **temporary**. They reduce risk but do not eliminate it. Always pursue patching as the ultimate resolution.

---

## 9. Tools and Technologies

### Vulnerability Management Platforms

| Tool | Description |
|------|-------------|
| **Tenable Nessus / Tenable.io** | Industry-leading vulnerability scanner |
| **Qualys VMDR** | Cloud-based vulnerability management |
| **Rapid7 InsightVM** | Vulnerability management with risk scoring |
| **OpenVAS** | Open-source vulnerability scanner |

### Patch Deployment Tools

| Tool | Environment |
|------|-------------|
| **Microsoft WSUS** | Windows Server Update Services — on-prem Windows patching |
| **Microsoft SCCM / Endpoint Manager (Intune)** | Enterprise Windows patching |
| **Red Hat Satellite** | RHEL/CentOS enterprise patching |
| **Ansible** | Agentless automation for Linux/Windows patching |
| **Chef / Puppet** | Configuration management and patch automation |
| **Jamf** | macOS and iOS device management and patching |

### Cloud-Native Patching

| Tool | Platform |
|------|----------|
| **AWS Systems Manager Patch Manager** | AWS EC2 instances |
| **Azure Update Management** | Azure VMs |
| **Google Cloud OS Patch Management** | GCP instances |

### Container Patching

Containers introduce unique challenges — the image itself may contain vulnerable software.

- **Trivy** — Open-source container image scanner
- **Snyk** — Developer-focused security scanning for containers and code
- **Anchore Engine** — Container image analysis and policy enforcement
- **Amazon ECR Image Scanning** — Built into AWS container registry

In container environments, "patching" means rebuilding the container image with updated base images or dependencies and redeploying.

---

## 10. Patch Management in Different Environments

### On-Premises (Traditional Data Center)

- Full control over patch timing
- Use WSUS, SCCM, Satellite, or Ansible
- Schedule maintenance windows
- Test in staging before production

### Cloud (IaaS — Infrastructure as a Service)

- **Shared Responsibility Model** — The cloud provider patches the hypervisor and physical infrastructure. You are responsible for patching the OS and software running on your VMs.
- Use cloud-native tools (AWS SSM, Azure Update Management)
- Leverage auto-scaling: terminate old unpatched instances and launch new patched ones (immutable infrastructure)

### Containers and Kubernetes

- Patch the base image (OS layer)
- Patch application dependencies (package managers inside the image)
- Rebuild and redeploy images
- Use image scanning in CI/CD pipelines to catch vulnerabilities before deployment
- Implement Kubernetes admission controllers to block deployment of images with known critical vulnerabilities

### Operational Technology (OT) / Industrial Control Systems (ICS)

OT patching is uniquely challenging because:
- Systems may run 24/7 with no tolerance for downtime
- Vendors may not release patches for legacy systems
- Patching can void warranties or violate industrial certifications
- The impact of a patch failure (taking down a power plant, factory line) may be severe

OT patch management requires:
- Extensive coordination with operations teams
- Longer testing periods
- Compensating controls when patches cannot be applied
- Vendor-specific guidance

### IoT (Internet of Things)

IoT devices are notoriously difficult to patch:
- Many have no update mechanism
- Vendors discontinue support rapidly
- Devices may be geographically distributed (sensors, cameras)
- Default credentials are common

Best practices:
- Inventory all IoT devices
- Segment IoT on a separate network
- Replace end-of-life devices that cannot be patched
- Use network monitoring to detect anomalous behavior

---

## 11. The Human Element: Culture and Process

### Patch Management Is a Team Sport

Effective patch management requires collaboration between:

- **Security Team** — Identifies vulnerabilities, sets risk priorities, defines SLAs
- **IT Operations / SysAdmins** — Deploys patches, manages maintenance windows
- **Development Teams** — Patches application dependencies and container images
- **Change Management** — Approves and schedules changes
- **Business Owners** — Approve downtime windows, balance risk vs. uptime
- **Leadership** — Allocates resources, sets risk appetite

### Common Human Failures

- **"It'll break something"** — Fear of patching causing an outage. Combat this with robust testing.
- **"We'll do it next cycle"** — Kicking the can. Dangerous when vulnerabilities are being actively exploited.
- **"We don't need to patch, we have a firewall"** — Defense-in-depth is important, but perimeter defenses alone are insufficient.
- **"That system is legacy, too risky to touch"** — Legacy systems with no patches are often the first compromised. Plan for migration.

### Building a Patch-Positive Culture

- Treat patch compliance as a key performance indicator visible to leadership
- Make patching easy — automate as much as possible to reduce friction
- Educate teams on real-world examples of unpatched vulnerabilities leading to breaches
- Celebrate good patch compliance rather than only penalizing non-compliance

---

## 12. Metrics and KPIs

Measure what matters. Key metrics for patch management programs:

### Operational Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **Patch Coverage** | % of assets with current patch status known | 100% |
| **Patch Compliance Rate** | % of systems patched within SLA by severity tier | >95% (Critical), >90% (High) |
| **Mean Time to Patch (MTTP)** | Average time from patch release to patch applied | < 24h (Critical), < 7d (High) |
| **Patch Failure Rate** | % of patch deployments that fail or require rollback | <5% |
| **Vulnerability Density** | Average number of unpatched vulnerabilities per asset | Trending down |

### Risk Metrics

| Metric | Description |
|--------|-------------|
| **Critical/High Vuln Age** | How old are your open critical/high vulnerabilities? |
| **SLA Breach Rate** | % of vulnerabilities not patched within defined SLA |
| **Assets with Actively Exploited Vulns** | Count of systems with CISA KEV entries unpatched |
| **Exposure Score** | Weighted risk score factoring asset criticality + vuln severity |

### Reporting Cadence

- **Weekly** — Operational metrics for IT/security teams
- **Monthly** — SLA compliance, trend analysis for security management
- **Quarterly** — Executive dashboard, risk posture, program maturity assessment
- **Annual** — Audit evidence, compliance reporting

---

## 13. Common Challenges and How to Overcome Them

### Challenge 1: Asset Discovery Gaps

**Problem:** You can't patch systems you don't know about.

**Solutions:**
- Implement continuous network scanning
- Integrate with cloud provider APIs to discover resources
- Use asset tagging in cloud environments
- Conduct periodic manual audits
- Deploy endpoint agents that report asset information

### Challenge 2: Legacy Systems

**Problem:** Old systems (Windows XP, Server 2003, EOL software) that no longer receive patches.

**Solutions:**
- Network isolation / air-gapping
- Application whitelisting
- Enhanced monitoring
- Plan and budget for migration
- Work with vendors for extended support (paid EOL support from Microsoft)

### Challenge 3: Patch Testing Delays

**Problem:** Testing takes weeks, extending the window of vulnerability.

**Solutions:**
- Automate regression testing
- Invest in test environment infrastructure
- Risk-tier your testing — critical patches get expedited testing
- Build a library of test cases that can be run quickly

### Challenge 4: Application Compatibility

**Problem:** Patching breaks business-critical applications.

**Solutions:**
- Work with application vendors to confirm patch compatibility
- Test patches against application workloads in staging
- Maintain application vendor contact for rapid testing support
- Use application virtualization or containers to isolate dependencies

### Challenge 5: Patch Fatigue

**Problem:** So many patches, so many systems — teams get overwhelmed.

**Solutions:**
- Risk-based prioritization — focus on what matters most
- Automate routine low-risk patches
- Consolidate tooling to reduce complexity
- Increase staffing or engage managed security service providers (MSSPs)

### Challenge 6: Distributed / Remote Endpoints

**Problem:** Laptops and endpoints that are rarely on the corporate network.

**Solutions:**
- Cloud-delivered patch management (Intune, Jamf)
- VPN-enforced patch compliance
- Direct internet access for update servers
- Conditional access policies that block non-compliant devices

---

## 14. Compliance and Regulatory Requirements

Many regulatory frameworks mandate patch management controls. Here is an overview:

### PCI DSS (Payment Card Industry Data Security Standard)

- **Requirement 6.3** — Security vulnerabilities are identified and addressed
- **Requirement 6.3.3** — All system components are protected from known vulnerabilities by installing applicable security patches/updates
- **SLA requirement:** Critical patches within 1 month of release

### HIPAA (Health Insurance Portability and Accountability Act)

- Under the **Security Rule**, covered entities must implement procedures to protect against malicious software and regularly review and modify security measures
- While HIPAA doesn't specify exact SLAs, patch management is a recognized best practice for compliance

### NIST Cybersecurity Framework (CSF)

- **ID.AM** (Asset Management) — Know what you have
- **PR.IP-12** — A vulnerability management plan is developed and implemented
- **DE.CM-8** — Vulnerability scans are performed

### ISO/IEC 27001

- **Annex A Control 8.8** — Management of technical vulnerabilities
- Requires timely identification, assessment, and remediation of technical vulnerabilities

### CISA BOD 22-01 (US Federal)

- **Binding Operational Directive 22-01** requires all US federal civilian agencies to remediate CISA Known Exploited Vulnerabilities (KEV) within defined timeframes (typically 2 weeks to 6 months depending on severity)

### SOC 2

- **Availability and Security Trust Service Criteria** include patch management as an expected control for service organizations

---

## 15. Zero-Day Vulnerabilities: When There Is No Patch

A **zero-day vulnerability** is a flaw that is unknown to the software vendor, meaning there is no patch available. The term comes from "zero days" of warning.

### Characteristics

- No vendor patch exists
- May already be actively exploited
- Typically disclosed by security researchers or discovered in-the-wild
- Often sold on dark web markets or by exploit brokers

### Response When There Is No Patch

When a zero-day affects your environment, your options are:

**1. Apply Vendor Workarounds**
Vendors often publish workarounds (configuration changes that disable the vulnerable feature) before a full patch is ready.

**2. Virtual Patching**
Deploy WAF rules, IPS signatures, or firewall rules that block known exploit patterns. These don't fix the vulnerability but prevent exploitation.

**3. Compensating Controls**
- Disable or isolate the vulnerable system
- Add additional authentication
- Increase logging and monitoring for exploitation attempts

**4. Network Segmentation**
Limit the attack surface by segmenting the vulnerable system from the rest of the network.

**5. Threat Hunt**
Actively search your environment for signs that the zero-day has already been exploited.

**6. Monitor and Wait**
For lower-risk systems, maintain heightened monitoring while waiting for an official patch.

> ⚠️ Zero-days highlight why **defense in depth** matters. An environment that relies solely on patching (perimeter defense) is vulnerable. Multiple layers of security reduce the impact of zero-days.

---

## 16. Patch Management Best Practices

### The Essentials

- ✅ **Maintain a complete and accurate asset inventory** — You cannot patch what you don't know about
- ✅ **Scan for vulnerabilities continuously** — Not just monthly; the threat landscape changes daily
- ✅ **Prioritize based on risk, not just CVSS** — Consider exploitability, asset criticality, and exposure
- ✅ **Never patch production directly** — Always test in a staging or lower environment first
- ✅ **Always have a rollback plan** — Document and test your rollback procedure before patching
- ✅ **Track CISA KEV** — Treat all known exploited vulnerabilities as P1 regardless of other factors
- ✅ **Automate where possible** — Reduce friction and human error with automation
- ✅ **Set and enforce SLAs** — Define, measure, and report on remediation timeframes
- ✅ **Include third-party and application patches** — OS patches alone are not enough
- ✅ **Document everything** — Patch history, decisions, exceptions, and risk acceptances

### Advanced Practices

- ✅ **Integrate vulnerability data with your CMDB** — Link vulnerabilities to business context
- ✅ **Implement patch management in CI/CD pipelines** — Catch vulnerabilities before deployment
- ✅ **Use immutable infrastructure** — Rebuild rather than patch (containers, cloud VMs)
- ✅ **Establish a formal exception process** — For systems that cannot be patched, document the risk acceptance, compensating controls, and remediation plan
- ✅ **Red team / penetration test** — Validate that your patch program is actually closing the doors attackers would use
- ✅ **Integrate threat intelligence** — Prioritize patches for vulnerabilities being actively exploited in your industry

---

## 17. Building a Patch Management Policy

A patch management policy is a formal document that defines the organization's approach. It should include:

### Policy Components

**1. Scope**
Define what is covered: all IT assets, OT systems, cloud resources, employee-owned devices (BYOD), etc.

**2. Roles and Responsibilities**
- Who owns the vulnerability management program?
- Who is responsible for patching each asset type?
- Who approves exceptions?
- Who reports to leadership?

**3. Asset Classification**
Define criticality tiers for systems (Critical, High, Medium, Low) based on business impact.

**4. Remediation SLAs**
Define mandatory timeframes for patching by severity:

```
Critical (CVSS 9.0+) ............... 24–48 hours
High (CVSS 7.0–8.9) ............... 7 days
Medium (CVSS 4.0–6.9) ............. 30 days
Low (CVSS < 4.0) .................. 90 days
CISA KEV (any score) .............. 14 days (or per CISA guidance)
```

**5. Testing Requirements**
Mandate that patches be tested before production deployment. Define test environments required.

**6. Exception Process**
- How to request an exception when a patch cannot be applied in time
- Required information: reason, risk assessment, compensating controls, target remediation date
- Who approves exceptions (risk owner + CISO)
- Maximum exception duration

**7. Reporting and Metrics**
Define what will be measured, how often, and who receives reports.

**8. Review Cycle**
Policy should be reviewed and updated at least annually, or after significant changes in the environment or threat landscape.

---

## 18. Glossary

| Term | Definition |
|------|------------|
| **APT** | Advanced Persistent Threat — sophisticated, long-term adversary (often nation-state) |
| **Asset Inventory** | A complete list of all IT assets in the environment |
| **CISA KEV** | CISA Known Exploited Vulnerabilities catalog — active exploits tracked by the US government |
| **CMDB** | Configuration Management Database — central repository of IT asset information |
| **Compensating Control** | A security control that reduces risk when the primary control cannot be applied |
| **CVE** | Common Vulnerabilities and Exposures — standardized vulnerability identifier |
| **CVSS** | Common Vulnerability Scoring System — numeric severity rating for vulnerabilities |
| **Defense in Depth** | Using multiple layers of security so no single failure leads to a breach |
| **End of Life (EOL)** | Software/hardware no longer supported by the vendor; no more patches |
| **EPSS** | Exploit Prediction Scoring System — probability a vulnerability will be exploited |
| **Exploit** | Code or technique that leverages a vulnerability to cause harm |
| **Hotfix** | An urgent, often unscheduled patch for a critical issue |
| **Immutable Infrastructure** | Infrastructure that is replaced rather than modified (e.g., containers) |
| **Patch Gap** | The time between patch release and when an organization applies it |
| **Penetration Testing** | Authorized simulated attack to test security controls |
| **Risk Acceptance** | A formal decision to accept the risk of not patching, with documentation |
| **SLA** | Service Level Agreement — defined timeframe for completing an action (e.g., patching) |
| **Threat Intelligence** | Information about current adversaries, tactics, and targeted vulnerabilities |
| **Virtual Patching** | Using WAF/IPS rules to block exploits without changing the vulnerable software |
| **Vulnerability** | A weakness in software or hardware that could be exploited |
| **WSUS** | Windows Server Update Services — Microsoft's on-premises patch distribution tool |
| **Zero-Day** | A vulnerability unknown to the vendor; no patch exists |

---

## Summary: Closing the Door

Patch management is ultimately about **reducing the attack surface** that adversaries exploit. Every unpatched vulnerability is a door left open. Every applied patch is a door closed.

The "art" lies in making smart decisions about which doors to close first, how to close them without disrupting the business, and what to do when a door cannot yet be closed.

The "science" lies in the systematic processes, tools, metrics, and automation that make closing doors reliable, measurable, and scalable across thousands of systems.

Organizations that do patch management well:
- Know every asset they have
- Know the vulnerabilities on each asset
- Prioritize ruthlessly based on real risk
- Patch fast for critical issues, systematically for everything else
- Measure their performance and continuously improve
- Treat patch management as a continuous program, not a one-time project

**The attackers are counting on you to have open doors. Don't.**

---

*Document maintained as part of the Security Knowledge Base.*
*Last reviewed: 2025 | Framework references: NIST CSF, PCI DSS v4.0, ISO 27001:2022, CISA KEV*
