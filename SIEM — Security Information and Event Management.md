# 🛡️ SIEM — Security Information and Event Management
### The SOC's Commanding Center: A Complete Technical Guide

---

## Table of Contents

1. [What is SIEM?](#1-what-is-siem)
2. [Why SIEM Matters](#2-why-siem-matters)
3. [Core Components of a SIEM](#3-core-components-of-a-siem)
4. [How SIEM Works — Data Flow](#4-how-siem-works--data-flow)
5. [SIEM and the SOC — The Commanding Center](#5-siem-and-the-soc--the-commanding-center)
6. [Key SIEM Use Cases](#6-key-siem-use-cases)
7. [Popular SIEM Tools](#7-popular-siem-tools)
8. [Splunk — Hands-On Walkthrough](#8-splunk--hands-on-walkthrough)
9. [IBM QRadar — Hands-On Walkthrough](#9-ibm-qradar--hands-on-walkthrough)
10. [Microsoft Sentinel — Hands-On Walkthrough](#10-microsoft-sentinel--hands-on-walkthrough)
11. [Elastic SIEM (ELK Stack) — Hands-On Walkthrough](#11-elastic-siem-elk-stack--hands-on-walkthrough)
12. [Writing SIEM Rules & Correlation Logic](#12-writing-siem-rules--correlation-logic)
13. [SIEM Metrics & KPIs](#13-siem-metrics--kpis)
14. [SIEM Best Practices](#14-siem-best-practices)
15. [Glossary](#15-glossary)

---

## 1. What is SIEM?

**SIEM** stands for **Security Information and Event Management**. It is a security solution that combines two older disciplines:

| Term | Full Name | What it Did |
|------|-----------|-------------|
| **SIM** | Security Information Management | Long-term log storage, compliance reporting |
| **SEM** | Security Event Management | Real-time monitoring, alerting, correlation |

Together, SIEM gives security teams a **single, unified platform** to:

- **Collect** security logs from every source in the environment
- **Normalize** disparate log formats into a standard schema
- **Correlate** events across multiple systems to detect threats
- **Alert** analysts when suspicious patterns are found
- **Store** data for forensic investigation and compliance audits

> 💡 **Simple analogy:** Imagine a city surveillance system. Each camera is a log source. SIEM is the central control room where all camera feeds are displayed, analyzed, and alerts are sent to officers when suspicious activity is detected.

---

## 2. Why SIEM Matters

Modern enterprise environments generate **millions of events per day** across thousands of devices. Without SIEM:

```
Firewall logs ──────────────────────────── Analyst #1 reads manually
Windows Event Logs ──────────────────────  Analyst #2 reads manually
Web Proxy logs ──────────────────────────  Analyst #3 reads manually
Endpoint Detection logs ─────────────────  Analyst #4 reads manually
DNS logs ────────────────────────────────  Nobody reads them
Cloud logs ──────────────────────────────  Nobody reads them
```

**With SIEM:**

```
All logs ──► SIEM Engine ──► Correlate ──► Alert ──► Analyst acts
```

### Business Drivers for SIEM

- **Compliance requirements:** PCI-DSS, HIPAA, SOX, GDPR, ISO 27001 all require log management and audit trails.
- **Threat detection:** Identify attacks that span multiple systems (lateral movement, data exfiltration).
- **Incident response:** Centralized investigation without logging into 50 different systems.
- **Mean Time to Detect (MTTD):** SIEM dramatically reduces how long attackers go undetected.
- **Mean Time to Respond (MTTR):** Faster investigation = faster containment.

---

## 3. Core Components of a SIEM

```
┌─────────────────────────────────────────────────────────────────────────┐
│                            SIEM PLATFORM                                │
│                                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐  │
│  │   Data       │  │  Parsing &   │  │ Correlation  │  │  Alerting  │  │
│  │  Collection  │─►│Normalization │─►│   Engine     │─►│   Engine   │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  └────────────┘  │
│         │                                                      │        │
│         ▼                                                      ▼        │
│  ┌──────────────┐                                    ┌──────────────┐   │
│  │  Long-term   │                                    │  Dashboard & │   │
│  │   Storage    │                                    │  Reporting   │   │
│  └──────────────┘                                    └──────────────┘   │
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────────┐   │
│  │                    Threat Intelligence Feed                      │   │
│  └──────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 3.1 Data Collection (Log Sources)

The SIEM ingests logs from **every possible source** in the environment. These are called **log sources** or **data sources**.

#### Categories of Log Sources

```
┌────────────────────────────────────────────────────────────┐
│                     LOG SOURCES                            │
├──────────────────┬─────────────────────────────────────────┤
│ NETWORK          │ Firewalls, Routers, Switches, IDS/IPS,  │
│                  │ VPN, DNS, DHCP, Proxy, Load Balancers   │
├──────────────────┼─────────────────────────────────────────┤
│ ENDPOINT         │ Windows Event Logs, Syslog (Linux/Mac), │
│                  │ EDR tools (CrowdStrike, SentinelOne)    │
├──────────────────┼─────────────────────────────────────────┤
│ APPLICATION      │ Web servers (Apache/Nginx/IIS),         │
│                  │ Databases (MySQL, MSSQL, Oracle),       │
│                  │ Custom application logs                 │
├──────────────────┼─────────────────────────────────────────┤
│ IDENTITY         │ Active Directory, LDAP, RADIUS,         │
│                  │ Okta, Azure AD, PAM solutions           │
├──────────────────┼─────────────────────────────────────────┤
│ CLOUD            │ AWS CloudTrail, Azure Monitor,          │
│                  │ GCP Audit Logs, Office 365, Salesforce  │
├──────────────────┼─────────────────────────────────────────┤
│ SECURITY TOOLS   │ Antivirus, DLP, WAF, Vulnerability      │
│                  │ Scanners, Email Security Gateways       │
└──────────────────┴─────────────────────────────────────────┘
```

#### How Logs Are Sent to SIEM

| Method | Description | Used By |
|--------|-------------|---------|
| **Syslog (UDP/TCP 514)** | Network devices push logs in real-time | Firewalls, switches, routers |
| **Agent-based** | Software installed on host that forwards logs | Windows/Linux endpoints |
| **API-based** | SIEM polls cloud service APIs | AWS, Azure, Office 365 |
| **Log file polling** | SIEM reads log files from network share | Legacy applications |
| **JDBC/ODBC** | Database log ingestion | MSSQL, Oracle |
| **Kafka/Message Queue** | High-volume streaming | Modern microservices |

---

### 3.2 Log Parsing and Normalization

Raw logs look different from every source. The **parser** transforms them into a consistent format.

#### Before Normalization (Raw Logs)

**Windows Event Log (raw):**
```
<Event xmlns='http://schemas.microsoft.com/win/2004/08/events/event'>
  <System>
    <EventID>4625</EventID>
    <TimeCreated SystemTime='2024-01-15T08:23:45.000Z'/>
    <Computer>WORKSTATION-01</Computer>
  </System>
  <EventData>
    <Data Name='TargetUserName'>john.doe</Data>
    <Data Name='IpAddress'>192.168.1.50</Data>
    <Data Name='Status'>0xC000006D</Data>
  </EventData>
</Event>
```

**Linux Syslog PAM (raw):**
```
Jan 15 08:23:45 server01 sshd[1234]: Failed password for john.doe from 192.168.1.50 port 54321 ssh2
```

#### After Normalization (Unified Schema)

| Field | Windows | Linux | Normalized Value |
|-------|---------|-------|-----------------|
| Timestamp | `2024-01-15T08:23:45Z` | `Jan 15 08:23:45` | `2024-01-15T08:23:45Z` |
| Event type | `EventID: 4625` | `Failed password` | `authentication_failure` |
| Username | `TargetUserName: john.doe` | `john.doe` | `john.doe` |
| Source IP | `IpAddress: 192.168.1.50` | `from 192.168.1.50` | `192.168.1.50` |
| Outcome | `Status: 0xC000006D` | `Failed` | `failure` |

This unified schema is what makes **correlation across sources** possible.

---

### 3.3 Correlation Engine

The **correlation engine** is the brain of the SIEM. It looks for patterns across multiple events that, individually, look benign but together indicate an attack.

#### How Correlation Works

```
Event 1: john.doe — login failure — 08:23:45 — from 192.168.1.50
Event 2: john.doe — login failure — 08:23:46 — from 192.168.1.50
Event 3: john.doe — login failure — 08:23:47 — from 192.168.1.50
Event 4: john.doe — login failure — 08:23:48 — from 192.168.1.50
Event 5: john.doe — login failure — 08:23:49 — from 192.168.1.50
        ↓
   Correlation Rule:
   "If same user + same IP fails > 5 times in 60 seconds"
        ↓
   🚨 ALERT: Brute-force attack detected!
   User: john.doe | Source: 192.168.1.50 | Severity: HIGH
```

#### Types of Correlation Rules

| Rule Type | Description | Example |
|-----------|-------------|---------|
| **Threshold** | Alert when count exceeds limit in time window | 10 failed logins in 60 seconds |
| **Sequence** | Events must happen in specific order | Recon → Exploit → Privilege Escalation |
| **Baseline Deviation** | Alert on unusual activity vs. normal behavior | Login at 3 AM when user always logs in at 9 AM |
| **Blacklist Match** | Alert when known bad indicator is seen | Known malicious IP communicates with internal host |
| **Velocity** | Rate of events is abnormal | 1,000 DNS queries per second (DNS tunneling) |
| **Cross-source** | Combine events from different systems | Firewall allowed + IDS detected + Antivirus missed |

---

### 3.4 Alerting and Case Management

When the correlation engine fires, SIEM creates an **alert** (also called an **offense**, **incident**, or **notable event** depending on the platform).

#### Alert Anatomy

```
╔══════════════════════════════════════════════════════════════════╗
║  🚨 ALERT: Brute Force Attack Followed by Successful Login       ║
╠══════════════════════════════════════════════════════════════════╣
║  Severity:     HIGH (8/10)                                       ║
║  Status:       NEW                                               ║
║  Rule:         BRUTE_FORCE_THEN_SUCCESS                          ║
║  Triggered:    2024-01-15 08:24:10 UTC                           ║
╠══════════════════════════════════════════════════════════════════╣
║  INVOLVED ASSETS                                                 ║
║  ├── Source IP:    192.168.1.50   (User: john.doe)               ║
║  └── Destination:  DC01.corp.local (Domain Controller)           ║
╠══════════════════════════════════════════════════════════════════╣
║  EVIDENCE (7 events)                                             ║
║  ├── [08:23:45] 5x Failed Login  → DC01 (EventID 4625)           ║
║  └── [08:24:08] 1x Successful Login → DC01 (EventID 4624)        ║
╠══════════════════════════════════════════════════════════════════╣
║  MITRE ATT&CK Mapping                                            ║
║  └── T1110.001 — Brute Force: Password Guessing                  ║
╚══════════════════════════════════════════════════════════════════╝
```

---

### 3.5 Long-Term Storage (Data Retention)

SIEM stores logs for:

- **Compliance:** PCI-DSS requires 12 months; HIPAA up to 7 years
- **Forensic investigation:** What happened 6 months ago?
- **Threat hunting:** Retroactive search for newly discovered IOCs

#### Storage Tiers

```
HOT Storage (0–30 days)
├── Fast SSD/NVMe
├── Fully indexed and searchable
└── Used for active investigations

WARM Storage (30–365 days)
├── Slower HDD or object storage
├── Compressed, partially indexed
└── Used for compliance queries

COLD/ARCHIVE Storage (1–7 years)
├── Object storage (S3, Azure Blob)
├── Compressed and encrypted
└── Retrieved on-demand only
```

---

### 3.6 Threat Intelligence Integration

SIEM platforms integrate with **Threat Intelligence feeds** to enrich alerts with context.

| Intelligence Type | Example | How SIEM Uses It |
|------------------|---------|-----------------|
| **IP Reputation** | Known botnet C2 server | Flag connections to malicious IPs |
| **Domain IOCs** | Phishing domains | Alert when internal hosts resolve them |
| **File Hashes** | Known malware hash | Alert when endpoint runs malicious file |
| **MITRE ATT&CK TTPs** | Technique ID T1059 | Map alerts to attacker techniques |
| **ISAC Feeds** | FS-ISAC for banking | Industry-specific threat sharing |

Feeds can be commercial (Recorded Future, CrowdStrike Intel) or free (MISP, AlienVault OTX, CISA KEV).

---

### 3.7 Dashboards and Reporting

SIEM provides visual dashboards for different audiences:

```
┌─────────────────── SOC DASHBOARD ──────────────────────────────┐
│                                                                 │
│  Events/Hour     Alerts Today     Open Cases    Avg MTTD        │
│  ┌──────────┐   ┌──────────┐    ┌──────────┐  ┌──────────┐    │
│  │  124,500 │   │   47     │    │   12     │  │  4.2 min │    │
│  └──────────┘   └──────────┘    └──────────┘  └──────────┘    │
│                                                                 │
│  Top Alert Categories          Severity Distribution           │
│  ┌────────────────────┐        ┌────────────────────────────┐  │
│  │ 🔴 Brute Force  18 │        │ Critical ████ 5%           │  │
│  │ 🟡 Malware Comm 12 │        │ High     ████████ 18%      │  │
│  │ 🟠 Policy Viol  10 │        │ Medium   ████████████ 47%  │  │
│  │ 🟢 Recon         7 │        │ Low      ██████████ 30%    │  │
│  └────────────────────┘        └────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4. How SIEM Works — Data Flow

```
┌─────────────────── DATA FLOW THROUGH SIEM ──────────────────────┐
│                                                                  │
│  DATA SOURCES         COLLECTION      PROCESSING     OUTPUT      │
│                                                                  │
│  [Firewall]  ─syslog──►┐                                        │
│  [Windows]   ─agent──►─┤             ┌──────────┐               │
│  [Linux]     ─syslog──►┤  ┌───────┐  │Correlation│  ┌────────┐  │
│  [AWS]       ─API────►─┤─►│Parser │─►│  Engine  │─►│ Alerts │  │
│  [Office365] ─API────►─┤  │  &    │  └──────────┘  └────────┘  │
│  [Database]  ─JDBC───►─┤  │Normaliz│       │                    │
│  [IDS]       ─syslog──►┘  └───────┘  ┌─────▼────┐  ┌────────┐  │
│                                       │   Risk   │  │Reports │  │
│                              ┌──────┐ │  Scoring │  │Dashbds │  │
│                              │Index │ └──────────┘  └────────┘  │
│                              │Store │       │                    │
│                              └──────┘  ┌────▼────┐              │
│                                        │  Case   │              │
│                                        │  Mgmt   │              │
│                                        └─────────┘              │
└──────────────────────────────────────────────────────────────────┘
```

### Step-by-Step Event Lifecycle

```
Step 1: EVENT GENERATED
└── A user logs into a server at 3 AM
    └── Windows generates EventID 4624 (Logon Success)

Step 2: LOG COLLECTED
└── SIEM agent on the server captures the Windows Event Log
    └── Sends via encrypted TCP to SIEM receiver (port 514 or custom)

Step 3: PARSED & NORMALIZED
└── SIEM parser extracts:
    ├── timestamp:    2024-01-15T03:14:23Z
    ├── user:         admin
    ├── src_ip:       10.0.5.100
    ├── dest_host:    PRODSERVER01
    ├── event_type:   authentication_success
    └── logon_type:   network (type 3)

Step 4: INDEXED & STORED
└── Event written to fast-search index with all normalized fields

Step 5: CORRELATION CHECK
└── Engine checks: "Does this match any active rules?"
    └── RULE MATCH: "Successful login outside business hours by admin"
        └── Severity: MEDIUM, rule: OFF_HOURS_ADMIN_LOGIN

Step 6: ALERT CREATED
└── Alert ticket created in SIEM case management
    └── Assigned to on-call analyst via email + Slack

Step 7: ANALYST INVESTIGATES
└── Analyst searches SIEM for all events from admin@10.0.5.100
    └── Finds: 3x failed logins before success (lateral movement?)
    └── Correlates with: VPN logs show login from new country

Step 8: RESPONSE & CLOSE
└── Analyst escalates → account suspended → IR investigation begins
    └── All findings documented in SIEM case timeline
```

---

## 5. SIEM and the SOC — The Commanding Center

The **Security Operations Center (SOC)** is the team responsible for monitoring, detecting, investigating, and responding to security events. **SIEM is the central command console of the SOC.**

### SOC Structure and SIEM Interaction

```
┌──────────────────────────────────────────────────────────────────┐
│                      SECURITY OPERATIONS CENTER                  │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │                    SIEM PLATFORM                            │ │
│  │         (The Commanding Center of the SOC)                  │ │
│  └─────────────────────────────────────────────────────────────┘ │
│            │               │               │                     │
│            ▼               ▼               ▼                     │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐           │
│  │  TIER 1     │  │   TIER 2     │  │   TIER 3      │           │
│  │  Analyst    │  │   Analyst    │  │   Analyst/IR  │           │
│  │             │  │             │  │               │           │
│  │ • Monitor   │  │ • Deep-dive │  │ • Threat Hunt │           │
│  │   dashboards│  │   analysis  │  │ • Forensics   │           │
│  │ • Triage    │  │ • Escalate  │  │ • IR Lead     │           │
│  │   alerts    │  │   criticals │  │ • SIEM Rule   │           │
│  │ • Close FPs │  │ • Write IOC │  │   Engineering │           │
│  └─────────────┘  └──────────────┘  └───────────────┘           │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  ADJACENT TEAMS THAT INTERACT WITH SIEM                    │  │
│  │  Threat Intel | Vulnerability Mgmt | Compliance | IT Ops  │  │
│  └────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

### SOC Analyst Daily Workflow with SIEM

```
🌅 START OF SHIFT
│
├── 1. Review overnight alert queue in SIEM
│       └── Triage by severity: Critical → High → Medium → Low
│
├── 2. Check SIEM dashboard
│       ├── Event ingestion rate (are all sources sending logs?)
│       ├── New alert count vs. previous day
│       └── Any infrastructure errors (missing log sources)
│
├── 3. Investigate each alert
│       ├── Open alert in SIEM
│       ├── Pivot to raw events behind the alert
│       ├── Search SIEM for additional context
│       │       └── What else has this IP done in the last 30 days?
│       ├── Enrich with Threat Intel (is IP/domain known bad?)
│       ├── Document findings in case
│       └── Determine: True Positive, False Positive, or Benign?
│
├── 4. True Positive → Escalate
│       └── Alert Tier 2 or trigger IR playbook
│
├── 5. False Positive → Tune
│       └── Work with Tier 3 to update SIEM rule (reduce noise)
│
└── 🌙 END OF SHIFT
        └── Hand off open cases with status notes
```

### SIEM as Integration Hub

```
                     ┌──────────────┐
     SOAR Platform ◄─┤              ├─► Ticketing System
     (auto-response) │              │   (ServiceNow, Jira)
                     │    SIEM      │
  Threat Intel  ────►│  Commanding  ├─► Email/Slack Alerts
  Feeds               │    Center   │
                     │              │
  Vulnerability  ────►│              ├─► Compliance Reports
  Scanners           │              │
                     └──────────────┘
```

---

## 6. Key SIEM Use Cases

### Use Case 1: Detecting Lateral Movement

**Scenario:** Attacker compromises one host and moves to others.

```
Detection Logic:
─────────────────
Time window: 30 minutes
Rule: Same source IP → successful authentication → 5+ DIFFERENT destination hosts

Evidence chain SIEM would collect:
[10:00] WORKSTATION-04 (10.0.1.44) → login SUCCESS → SERVER-01
[10:05] WORKSTATION-04 (10.0.1.44) → login SUCCESS → SERVER-02
[10:08] WORKSTATION-04 (10.0.1.44) → login SUCCESS → SERVER-03
[10:12] WORKSTATION-04 (10.0.1.44) → login SUCCESS → DC-01 ← 🚨 ALERT
```

---

### Use Case 2: Data Exfiltration Detection

```
Detection Logic:
─────────────────
Rule: Internal host → large data transfer (>500MB) → external IP
AND: Destination IP not in approved cloud services list

SIEM correlates:
  Proxy log:  10.0.5.22 → 185.220.101.1  (TOR exit node) → 1.2 GB
  DLP Alert:  10.0.5.22 → bulk file download from SharePoint
  
→ 🚨 ALERT: Data Exfiltration Attempt — CRITICAL
```

---

### Use Case 3: Ransomware Detection

```
Behavioral chain SIEM detects:
────────────────────────────────
Event 1: PowerShell execution with encoded command (EventID 4104)
Event 2: Mass file access on file server (>1000 files in 60s)
Event 3: Files renamed with unknown extension (.locked, .encrypted)
Event 4: Shadow copies deleted (vssadmin delete shadows)
Event 5: New scheduled task created for persistence

→ 🚨 CRITICAL ALERT: RANSOMWARE BEHAVIOR DETECTED
   Isolate host immediately! Run IR playbook!
```

---

### Use Case 4: Impossible Travel / Account Compromise

```
Logic:
──────
User logs in from New York at 09:00 (IP geo: New York, USA)
Same user logs in from Lagos at 09:45 (IP geo: Lagos, Nigeria)

Time difference: 45 minutes
Physical distance: ~8,000 km (impossible to travel in 45 min)

→ 🚨 ALERT: Impossible Travel — Account johndoe@corp.com likely compromised
```

---

## 7. Popular SIEM Tools

| SIEM Tool | Vendor | Best For | Pricing Model |
|-----------|--------|----------|---------------|
| **Splunk Enterprise Security** | Splunk (Cisco) | Large enterprises, mature SOCs | GB/day ingestion |
| **IBM QRadar** | IBM | Enterprise, telecoms, finance | EPS (Events Per Second) |
| **Microsoft Sentinel** | Microsoft | Azure-heavy environments | GB/day ingested |
| **Elastic SIEM** | Elastic | Cost-sensitive, custom needs | Node-based or SaaS |
| **LogRhythm** | LogRhythm | Mid-size enterprise | EPS + MPS |
| **Exabeam** | Exabeam | UEBA-focused, behavior analytics | User-based |
| **ArcSight** | Micro Focus | Government, compliance-heavy | EPS |
| **AlienVault OSSIM** | AT&T Cybersecurity | Small teams, open source | Free / USM paid |
| **Wazuh** | Wazuh Inc. | Open source, budget SOCs | Free (self-hosted) |
| **Chronicle SIEM** | Google Cloud | Cloud-native, petabyte scale | Capacity-based |

---

## 8. Splunk — Hands-On Walkthrough

Splunk is one of the most widely deployed SIEM platforms. It uses a powerful search language called **SPL (Search Processing Language)**.

### 8.1 Splunk Architecture

```
┌───────────────────────────────────────────────────┐
│                  SPLUNK DEPLOYMENT                │
│                                                   │
│  Data Sources → [Universal Forwarders]            │
│                        │                         │
│                        ▼                         │
│              [Heavy Forwarder / Indexer]          │
│              (Receives, Parses, Indexes)          │
│                        │                         │
│                        ▼                         │
│              [Search Head]                        │
│              (Web UI, SPL queries, Dashboards)    │
│                        │                         │
│              [Splunk ES App] ← Enterprise Security│
└───────────────────────────────────────────────────┘
```

### 8.2 Navigating the Splunk Web UI

```
SPLUNK NAVIGATION (Web UI at http://splunk:8000)
───────────────────────────────────────────────
Top Menu Bar:
  ├── Search & Reporting     ← Main search interface
  ├── Dashboards             ← Visual panels
  ├── Alerts                 ← Triggered alert rules
  ├── Reports                ← Saved queries
  └── App: Enterprise Security ← SIEM-specific app

Search Bar (core element):
  ┌────────────────────────────────────────────────┐
  │ index=windows EventCode=4625                   │
  │ | stats count by src_ip, user                 │
  │ | where count > 5                             │
  └────────────────────────────────────────────────┘
  Time picker: [Last 24 hours ▼]  [🔍 Search]
```

#### Screenshot Description — Splunk Search Interface
```
╔══════════════════════════════════════════════════════════════════════╗
║  SPLUNK ENTERPRISE SECURITY — Search                                 ║
╠══════════════════════════════════════════════════════════════════════╣
║  [Search bar: index=windows EventCode=4625 | stats count by src_ip] ║
║  Time: Last 24 hours                              [Search]           ║
╠══════════════════════════════════════════════════════════════════════╣
║  RESULTS (143,200 events matched)                                    ║
║                                                                      ║
║  src_ip           count   user                                       ║
║  ─────────────────────────────────────────────                       ║
║  192.168.1.50       423   john.doe     ← 🚨 Anomaly!                ║
║  10.0.5.100          12   jane.smith                                 ║
║  172.16.0.25          8   bob.jones                                  ║
║                                                                      ║
║  [Visualization] [Events] [Statistics] [Export]                     ║
╚══════════════════════════════════════════════════════════════════════╝
```

### 8.3 SPL Query Examples

#### Search for Failed Logins (Windows)
```spl
index=windows EventCode=4625
| stats count as failures by src_ip, user
| where failures > 10
| sort -failures
| table src_ip, user, failures
```

#### Detect Brute Force — Full Correlation
```spl
index=windows (EventCode=4625 OR EventCode=4624)
| eval event_type=if(EventCode=4625, "failure", "success")
| stats
    count(eval(event_type="failure")) as fail_count,
    count(eval(event_type="success")) as success_count
    by src_ip, user, span=1h
| where fail_count > 5 AND success_count > 0
| eval alert_message = "Brute force followed by successful login"
| table src_ip, user, fail_count, success_count, alert_message
```

#### Hunt for PowerShell Encoded Commands (Malware)
```spl
index=windows EventCode=4104
| search ScriptBlockText="*-EncodedCommand*" OR ScriptBlockText="*-enc *"
| stats count by Computer, User, ScriptBlockText
| sort -count
```

#### Network Exfiltration Detection (Proxy Logs)
```spl
index=proxy
| stats sum(bytes_out) as total_bytes_out by src_ip, dest_domain
| eval GB_out = round(total_bytes_out/1073741824, 2)
| where GB_out > 1
| lookup threat_intel dest_domain OUTPUT category, is_malicious
| table src_ip, dest_domain, GB_out, category, is_malicious
```

#### Impossible Travel Detection
```spl
index=auth sourcetype=okta action=success
| iplocation src_ip
| stats
    values(src_ip) as ips,
    values(City) as cities,
    values(Country) as countries,
    earliest(_time) as first_login,
    latest(_time) as last_login
    by user
| where mvcount(countries) > 1
| eval time_diff_minutes = round((last_login - first_login)/60, 1)
| where time_diff_minutes < 120
| table user, cities, countries, time_diff_minutes, ips
```

### 8.4 Creating a Splunk Alert

```
HOW TO CREATE AN ALERT IN SPLUNK
─────────────────────────────────

1. Run your SPL search query
2. Click "Save As" → "Alert"
3. Fill in alert details:

   Title:       Brute Force Attack Detected
   Description: 5+ failed logins from same IP in 60 minutes
   
   Alert Type:  ● Scheduled  ○ Real-time
   Schedule:    Run Every: [5 minutes ▼]
   
   Trigger Conditions:
   ● Number of results  [is greater than ▼]  [0]
   
   Trigger Actions:
   ☑ Send email → soc-team@company.com
   ☑ Run script → create_case.py
   ☑ Add to Triggered Alerts

4. Click "Save"
```

---

## 9. IBM QRadar — Hands-On Walkthrough

IBM QRadar is an enterprise SIEM with deep packet inspection and automatic **offense** creation.

### 9.1 QRadar Architecture

```
┌──────────────────────────────────────────────────┐
│                 QRADAR DEPLOYMENT                │
│                                                  │
│  Log Sources → [Event Collector]                 │
│                      │                          │
│              [Event Processor]                   │
│              (Normalizes, Correlates)            │
│                      │                          │
│              [QRadar Console]                    │
│              (Web UI, Offenses, Rules)           │
│                      │                          │
│    ┌─────────────────┴──────────────────┐        │
│    │   Flow Collector                   │        │
│    │   (Network flow analysis - QFlow)  │        │
│    └────────────────────────────────────┘        │
└──────────────────────────────────────────────────┘
```

### 9.2 QRadar Offenses Dashboard

```
╔═════════════════════════════════════════════════════════════════╗
║  IBM QRadar — Offenses Dashboard                                ║
╠═════════════════════════════════════════════════════════════════╣
║  [All Offenses ▼] [Last 24h ▼]  [Search...]                     ║
╠══════╦════════════════════════════════════╦════════╦════════════╣
║  ID  ║  Description                       ║ Mag.   ║ Status     ║
╠══════╬════════════════════════════════════╬════════╬════════════╣
║  447 ║ Brute Force Login: john.doe        ║  ████8 ║ OPEN       ║
║  446 ║ Malware Comm: 10.0.5.22 → TOR      ║  ████7 ║ IN PROG    ║
║  445 ║ Policy Violation: USB detected     ║  ███5  ║ CLOSED     ║
║  444 ║ Recon: Port Scan from 192.168.1.9  ║  ██4   ║ OPEN       ║
╚══════╩════════════════════════════════════╩════════╩════════════╝

  Magnitude Scale: 1 (low) → 10 (critical)
  Calculated from: Relevance × Severity × Credibility
```

### 9.3 QRadar AQL Query Language

QRadar uses **AQL (Ariel Query Language)** for searching:

```sql
-- Find all failed logins
SELECT
    username,
    sourceip,
    destinationip,
    COUNT(*) AS fail_count
FROM events
WHERE
    LOGSOURCETYPENAME(devicetype) = 'Microsoft Windows Security Event Log'
    AND eventid = 4625
    AND STARTTIME > NOW() - 1 HOURS
GROUP BY username, sourceip, destinationip
HAVING fail_count > 5
ORDER BY fail_count DESC
LAST 60 MINUTES
```

```sql
-- Detect DNS Tunneling (high query rate)
SELECT
    sourceip,
    destinationip,
    COUNT(*) AS dns_count,
    AVG(payloadlength) AS avg_payload
FROM events
WHERE
    applicationname = 'DNS'
    AND destinationport = 53
GROUP BY sourceip, destinationip
HAVING dns_count > 500 OR avg_payload > 100
LAST 5 MINUTES
```

### 9.4 QRadar Rule Creation

```
QRadar Rule Builder (Menu: Offenses → Rules → Add Rule)
──────────────────────────────────────────────────────

Rule Type: Event
Rule Name: Brute Force - Windows Login

WHEN the following events occur:
  ┌────────────────────────────────────────────────────┐
  │ AND when the event(s) were detected by one or more │
  │ of the following log source types:                 │
  │   [Microsoft Windows Security Event Log]           │
  │                                                    │
  │ AND when the event(s) matches:                     │
  │   EventID is any of [4625]                         │
  │                                                    │
  │ AND when these events are seen:                    │
  │   MORE THAN [5] times                              │
  │   IN [60] seconds                                  │
  │   across the same [Username] [Source IP]           │
  └────────────────────────────────────────────────────┘

ACTIONS when rule triggers:
  ☑ Create an Offense
  ☑ Set offense name: Brute Force — %USERNAME% from %SOURCEIP%
  ☑ Notify via email: soc@company.com
```

---

## 10. Microsoft Sentinel — Hands-On Walkthrough

Microsoft Sentinel is a **cloud-native SIEM** built on Azure. It's ideal for organizations using Microsoft 365, Azure, and hybrid environments.

### 10.1 Sentinel Architecture

```
┌──────────────────────────────────────────────────────┐
│             MICROSOFT SENTINEL (Azure)               │
│                                                      │
│  Data Sources → [Data Connectors]                    │
│                      │                              │
│              [Log Analytics Workspace]               │
│              (Stores all logs — Azure backbone)      │
│                      │                              │
│       ┌──────────────┼──────────────┐               │
│       ▼              ▼              ▼               │
│  [Analytics    [Incidents]   [Hunting]              │
│   Rules]       (Alerts +     (Proactive             │
│   (KQL)         Cases)        search)               │
│       │                                             │
│       └──► [Automation / SOAR Playbooks]            │
└──────────────────────────────────────────────────────┘
```

### 10.2 Connecting Data Sources

```
SENTINEL — Data Connectors
───────────────────────────
Menu: Sentinel → Data Connectors

Available Connectors:
┌──────────────────────────────────────────────────────┐
│ MICROSOFT SERVICES (Native — no agent needed)        │
│  ☑ Microsoft Defender for Endpoint                  │
│  ☑ Azure Active Directory (Sign-ins, Audit)         │
│  ☑ Microsoft 365 (Exchange, SharePoint, Teams)      │
│  ☑ Azure Activity (Resource changes)                │
│                                                      │
│ THIRD-PARTY (via CEF/Syslog agent)                   │
│  ○ Palo Alto Networks                               │
│  ○ Cisco ASA / Firepower                            │
│  ○ Fortinet                                         │
│  ○ AWS CloudTrail                                   │
└──────────────────────────────────────────────────────┘

Click connector → "Open connector page" → Follow setup guide
```

### 10.3 KQL Queries in Sentinel

Sentinel uses **KQL (Kusto Query Language)**:

```kql
// Detect Brute Force Attacks
SecurityEvent
| where EventID == 4625
| where TimeGenerated > ago(1h)
| summarize
    FailCount = count(),
    AccountList = make_set(TargetUserName)
    by IpAddress, bin(TimeGenerated, 5m)
| where FailCount > 10
| project TimeGenerated, IpAddress, FailCount, AccountList
| order by FailCount desc
```

```kql
// Suspicious PowerShell — Encoded Commands
SecurityEvent
| where EventID == 4104
| where ScriptBlockText has_any ("-EncodedCommand", "-Enc ", "FromBase64String")
| project TimeGenerated, Computer, Account, ScriptBlockText
| order by TimeGenerated desc
```

```kql
// Impossible Travel
let travel_threshold_minutes = 120;
SigninLogs
| where ResultType == 0  // Success
| extend City = tostring(LocationDetails.city)
| extend Country = tostring(LocationDetails.countryOrRegion)
| summarize
    locations = make_list(pack("City", City, "Country", Country, "Time", TimeGenerated, "IP", IPAddress))
    by UserPrincipalName
| mv-expand locations
| summarize
    distinct_countries = dcount(tostring(locations.Country)),
    first_login = min(todatetime(locations.Time)),
    last_login = max(todatetime(locations.Time))
    by UserPrincipalName
| extend travel_time_minutes = datetime_diff('minute', last_login, first_login)
| where distinct_countries > 1 and travel_time_minutes < travel_threshold_minutes
```

### 10.4 Creating a Sentinel Analytics Rule

```
CREATING AN ANALYTICS RULE IN SENTINEL
──────────────────────────────────────
Menu: Sentinel → Analytics → Create → Scheduled Query Rule

STEP 1 — General:
  Name:        Brute Force Password Attack
  Description: Detects 10+ failed logins from single IP in 5 minutes
  Severity:    High
  Tactics:     Credential Access (MITRE ATT&CK)

STEP 2 — Set Rule Logic (KQL):
  ┌─────────────────────────────────────────────────────────┐
  │ SecurityEvent                                           │
  │ | where EventID == 4625                                 │
  │ | summarize count() by IpAddress, bin(TimeGenerated,5m) │
  │ | where count_ > 10                                     │
  └─────────────────────────────────────────────────────────┘

  Run query every: 5 minutes
  Lookup data from last: 5 minutes

STEP 3 — Incident Settings:
  ☑ Create incidents from alerts triggered by this rule
  Group alerts into single incident: by IpAddress

STEP 4 — Automated Response:
  Add automation rule: "Run Playbook: Block-IP-in-Firewall"

STEP 5 — Review and Create
```

---

## 11. Elastic SIEM (ELK Stack) — Hands-On Walkthrough

**Elastic SIEM** is built on the ELK stack (Elasticsearch, Logstash, Kibana) with the **Elastic Security** app providing SIEM capabilities.

### 11.1 ELK Stack Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   ELK SIEM STACK                        │
│                                                         │
│  Log Sources → [Beats / Logstash]  ← Data Shippers     │
│       Filebeat (log files)                              │
│       Winlogbeat (Windows Events)                       │
│       Packetbeat (network packets)                      │
│       Metricbeat (metrics)                              │
│                    │                                    │
│              [Elasticsearch]  ← Storage + Search       │
│              (Indexed data store, DSL queries)          │
│                    │                                    │
│              [Kibana + Elastic Security App]            │
│              (Dashboards, Alerts, Timelines)            │
└─────────────────────────────────────────────────────────┘
```

### 11.2 Installing Elastic SIEM (Self-Hosted Quick Start)

```bash
# Step 1: Install Elasticsearch
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
sudo apt-get install elasticsearch

# Step 2: Start Elasticsearch
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch

# Verify it's running:
curl http://localhost:9200
# Expected: {"name": "your-node", "cluster_name": "elasticsearch", "version": {...}}

# Step 3: Install Kibana
sudo apt-get install kibana
sudo systemctl enable kibana
sudo systemctl start kibana
# UI accessible at: http://localhost:5601

# Step 4: Install Winlogbeat on Windows Endpoint
# Download from: https://www.elastic.co/downloads/beats/winlogbeat
# winlogbeat.yml config:
output.elasticsearch:
  hosts: ["https://siem-server:9200"]
  username: "winlogbeat_user"
  password: "your_password"

winlogbeat.event_logs:
  - name: Security
    event_id: 4624, 4625, 4648, 4688, 4698, 4720, 4726
  - name: System
  - name: Application

# Start the service:
.\install-service-winlogbeat.ps1
Start-Service winlogbeat
```

### 11.3 Elastic Security — Detection Rules

Elastic comes with 600+ pre-built detection rules. You can also write custom ones:

```
CREATING A CUSTOM DETECTION RULE IN ELASTIC SECURITY
──────────────────────────────────────────────────────
Menu: Security → Detections → Manage Rules → Create New Rule

Rule Type: ● Threshold  ○ EQL  ○ Machine Learning

Index patterns: winlogbeat-*, logs-windows.*

Query (KQL):
  event.code: "4625" and winlog.event_data.LogonType: "3"

Threshold:
  Threshold field: source.ip
  Threshold value: 10
  Time window:     5 minutes

Rule Details:
  Name:     Brute Force — Network Logon Failures
  Severity: High
  Risk Score: 73
  MITRE ATT&CK:
    Tactic: Credential Access
    Technique: T1110 — Brute Force
```

### 11.4 EQL (Event Query Language) in Elastic

EQL is powerful for sequence-based detection:

```eql
/* Detect command and control communication pattern */
sequence by host.name with maxspan=30s
  [process where event.type == "start" and
   process.name in ("powershell.exe", "cmd.exe", "wscript.exe")]
  [network where event.type == "start" and
   not destination.ip in ("10.0.0.0/8", "172.16.0.0/12", "192.168.0.0/16")]
```

```eql
/* Detect ransomware behavior: mass file rename */
sequence by host.name with maxspan=2m
  [process where event.type == "start" and
   process.name in ("powershell.exe", "wscript.exe")]
  [file where event.type == "change" and
   file.extension in ("locked", "encrypted", "crypted", "crypt")]
   with runs=50
```

---

## 12. Writing SIEM Rules & Correlation Logic

### 12.1 Rule Design Methodology

```
RULE DESIGN PROCESS
────────────────────

1. DEFINE THE THREAT
   What attacker behavior are you trying to detect?
   Example: "Password spraying — attacker tries one password
             against many accounts"

2. MAP TO LOG SOURCES
   What logs capture this behavior?
   Example: Windows Event Log (4625), Azure AD SigninLogs

3. IDENTIFY DISTINGUISHING ATTRIBUTES
   What makes this stand out from normal behavior?
   Example: Same source IP, MANY different usernames, low fail rate per user

4. WRITE THE LOGIC
   Threshold/sequence/baseline in your SIEM's query language

5. TEST AND TUNE
   Run against historical data
   What's the false positive rate?
   Tune thresholds until acceptable

6. DOCUMENT
   Rule name, description, MITRE mapping, severity, response steps
```

### 12.2 MITRE ATT&CK Mapping

Always map SIEM rules to the MITRE ATT&CK framework:

```
MITRE ATT&CK TACTIC → TECHNIQUE → SIEM RULE EXAMPLES
──────────────────────────────────────────────────────

INITIAL ACCESS (TA0001)
  └── T1566.001 Spearphishing Attachment
       → Rule: Email with executable attachment received

EXECUTION (TA0002)
  └── T1059.001 PowerShell
       → Rule: PowerShell with EncodedCommand flag

PERSISTENCE (TA0003)
  └── T1053.005 Scheduled Task
       → Rule: New scheduled task created (EventID 4698)

PRIVILEGE ESCALATION (TA0004)
  └── T1078 Valid Accounts
       → Rule: Admin login outside business hours

DEFENSE EVASION (TA0005)
  └── T1070.001 Clear Windows Event Logs
       → Rule: Event log cleared (EventID 1102)

CREDENTIAL ACCESS (TA0006)
  └── T1110 Brute Force
       → Rule: 10+ failed logins in 60 seconds

DISCOVERY (TA0007)
  └── T1046 Network Service Scanning
       → Rule: Port scan from internal host

LATERAL MOVEMENT (TA0008)
  └── T1021.002 SMB/Windows Admin Shares
       → Rule: Access to ADMIN$ or C$ shares

COLLECTION (TA0009)
  └── T1560.001 Archive via Utility
       → Rule: 7zip/WinRAR compressing large dirs

EXFILTRATION (TA0010)
  └── T1048 Exfiltration Over Alternative Protocol
       → Rule: Large DNS queries / DNS tunneling

IMPACT (TA0040)
  └── T1486 Data Encrypted for Impact
       → Rule: Ransomware behavior (mass file renames)
```

---

## 13. SIEM Metrics & KPIs

Track these metrics to measure your SOC's effectiveness:

| Metric | Formula | Target |
|--------|---------|--------|
| **MTTD** (Mean Time to Detect) | Avg time from attack start to SIEM alert | < 60 min |
| **MTTR** (Mean Time to Respond) | Avg time from alert to containment | < 4 hours |
| **True Positive Rate** | True alerts / Total alerts | > 80% |
| **False Positive Rate** | False alerts / Total alerts | < 20% |
| **Alert Volume** | Total alerts per day | Baseline & monitor |
| **SIEM Coverage** | % of systems sending logs | > 95% |
| **Log Source Health** | % of expected sources reporting | > 99% |
| **Events Per Second (EPS)** | Avg log ingestion rate | Monitor vs. license |

```
SIEM HEALTH DASHBOARD
──────────────────────

Log Source Status:
  ✅ Windows Domain Controllers     (4/4 online)
  ✅ Network Firewalls              (6/6 online)
  ⚠️  Linux Servers                 (47/50 online) ← 3 missing!
  ✅ Cloud (Azure AD)               (connected)
  ✅ EDR (CrowdStrike)              (connected)

Today's Stats:
  Events ingested:    12,450,000
  Alerts generated:   52
  True positives:     41  (79%)
  False positives:    11  (21%)
  Open incidents:     8
  MTTD average:       6.2 minutes
  MTTR average:       34 minutes
```

---

## 14. SIEM Best Practices

### ✅ Do's

```
1. LOG EVERYTHING IMPORTANT
   Prioritize: Auth logs, network flows, endpoint process creation,
   DNS, cloud API calls, database queries

2. NORMALIZE AND ENRICH
   Add asset context (is this a critical server?),
   user context (is this an admin account?),
   and threat intel enrichment

3. TUNE AGGRESSIVELY
   A noisy SIEM creates alert fatigue.
   Review false positives weekly and tune rules.

4. USE MITRE ATT&CK AS YOUR COMPASS
   Map all rules to ATT&CK. Identify gaps in coverage.

5. AUTOMATE TIER 1 RESPONSES
   Use SOAR (Security Orchestration) to auto-block IPs,
   disable accounts, or isolate hosts on high-confidence rules.

6. MAINTAIN LOG SOURCE HEALTH MONITORING
   Alert when a critical log source goes silent for > 5 minutes.

7. DOCUMENT EVERYTHING
   Rules, playbooks, tuning decisions, case notes.

8. CONDUCT PURPLE TEAM EXERCISES
   Simulate attacks and verify SIEM detects them.
   Fix gaps found.
```

### ❌ Don'ts

```
1. DON'T COLLECT LOGS WITHOUT A DETECTION PURPOSE
   Every GB costs money. Prioritize quality over quantity.

2. DON'T IGNORE ALERT FATIGUE
   If analysts are closing alerts without reading them, you have too many.

3. DON'T SKIP TUNING AFTER GO-LIVE
   New environments need 90 days of continuous tuning.

4. DON'T RELY ON SIEM ALONE
   SIEM + EDR + NDR + UEBA = layered defense. SIEM is the center, not the whole.

5. DON'T FORGET INSIDER THREATS
   SIEM rules often focus on external attackers. Tune for malicious insiders too.

6. DON'T NEGLECT CLOUD
   Modern attacks often start in cloud environments. Connect all cloud sources.
```

---

## 15. Glossary

| Term | Definition |
|------|-----------|
| **Alert** | Notification generated when a correlation rule fires |
| **AQL** | Ariel Query Language — IBM QRadar's search language |
| **Baseline** | Normal behavior profile used to detect anomalies |
| **CEF** | Common Event Format — standardized log format (ArcSight) |
| **Correlation** | Finding relationships between events across sources |
| **EPS** | Events Per Second — SIEM licensing and performance metric |
| **EQL** | Event Query Language — Elastic's sequence detection language |
| **False Positive** | Alert that triggered on benign activity |
| **IOC** | Indicator of Compromise — known-bad artifact (IP, hash, domain) |
| **KQL** | Kusto Query Language — Microsoft Sentinel's search language |
| **LEEF** | Log Event Extended Format — IBM QRadar's log format |
| **Log Source** | Any system sending logs to SIEM |
| **MTTD** | Mean Time to Detect — time from incident start to detection |
| **MTTR** | Mean Time to Respond — time from detection to containment |
| **Normalization** | Converting different log formats into a common schema |
| **Offense** | IBM QRadar's term for a correlated alert/incident |
| **Playbook** | Documented step-by-step procedure for responding to an alert |
| **SOC** | Security Operations Center |
| **SOAR** | Security Orchestration, Automation and Response |
| **SPL** | Search Processing Language — Splunk's query language |
| **TTP** | Tactics, Techniques, and Procedures (attacker behaviors) |
| **UEBA** | User and Entity Behavior Analytics |

---

## Quick Reference: SIEM Query Cheat Sheet

```
SPLUNK (SPL)                          QRADAR (AQL)
──────────────────────                ──────────────────────────────
index=windows EventCode=4625          SELECT sourceip, username, COUNT(*)
| stats count by src_ip               FROM events
| where count > 10                    WHERE eventid = 4625
                                      GROUP BY sourceip, username
                                      HAVING COUNT(*) > 10
                                      LAST 60 MINUTES

SENTINEL (KQL)                        ELASTIC (KQL/EQL)
──────────────────────                ──────────────────────────────
SecurityEvent                         event.code: "4625"
| where EventID == 4625               | stats count by source.ip, user.name
| summarize count()                     where count > 10
    by IpAddress
| where count_ > 10
```

---

*Document Version: 1.0 | Classification: Internal SOC Reference | Last Updated: 2024*
*References: MITRE ATT&CK Framework, NIST SP 800-92, CIS SIEM Best Practices*
