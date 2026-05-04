# Defense in Depth: SOC-Oriented Security Architecture

## Overview

**Defense in Depth** is a multi-layered security strategy designed to protect systems against sophisticated and evolving threats. Each layer contributes to:

- Prevention
- Detection
- Response
- Recovery

This model aligns strongly with:
- NIST Cybersecurity Framework (Identify, Protect, Detect, Respond, Recover)
- MITRE ATT&CK (Tactics, Techniques, and Procedures - TTPs)

---

## 🧱 Security Layers Mapped to Frameworks

| Layer                     | NIST Function | MITRE ATT&CK Focus                |
|--------------------------|--------------|----------------------------------|
| Physical Security        | Protect      | Initial Access                   |
| Network Security         | Detect       | Command & Control, Lateral Movement |
| Endpoint Security        | Detect       | Execution, Persistence           |
| Identity & Access Mgmt   | Protect      | Privilege Escalation             |
| Application Security     | Protect      | Exploitation                     |
| Data Security            | Protect      | Exfiltration                     |
| Logging & Monitoring     | Detect       | All Tactics                      |
| Incident Response        | Respond      | Incident Handling                |

---

## 🔐 Physical Security

### Objective:
Prevent unauthorized physical access to infrastructure.

### Controls:
- Biometric authentication
- Smart access cards
- CCTV with logging and retention
- Secure server rooms

### Threat Mapping:
- MITRE: **Initial Access (T1078 - Valid Accounts)**

### SOC Use Case:
Unauthorized badge access → Trigger alert → Investigate entry logs

---

## 🌐 Network Security

### Objective:
Control and monitor traffic across network boundaries.

### Technologies:
- Firewalls (stateful, NGFW)
- IDS/IPS (Snort, Suricata)
- VPN (IPSec, SSL VPN)

### Detection Focus:
- Traffic anomalies
- Beaconing behavior
- Suspicious DNS queries

### MITRE Mapping:
- Command & Control (T1071)
- Lateral Movement (T1021)

### Example Detection Rule:
