# NIST CSF Incident Response Playbook

![Security](https://img.shields.io/badge/Security-Incident%20Response-blue)
![Framework](https://img.shields.io/badge/Framework-NIST%20CSF-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

## Overview

A structured incident response playbook for three common security incidents, mapped to the **NIST Cybersecurity Framework (CSF)**. This project demonstrates understanding of the incident response lifecycle, security operations workflow, and industry-standard frameworks used in real SOC environments.

> Phishing scenarios validated through hands-on analysis on TryHackMe (Phishing Analysis Fundamentals).

---

## Incidents Covered

| Playbook | Severity Range | NIST Functions Covered |
|----------|---------------|----------------------|
| [Phishing Attack](playbook/playbook-phishing.md) | Low → High | Identify, Protect, Detect, Respond, Recover |
| [Brute Force Attack](playbook/playbook-brute-force.md) | Medium → Critical | Identify, Detect, Respond, Recover |
| [Insider Threat](playbook/playbook-insider-threat.md) | High → Critical | Identify, Protect, Detect, Respond, Recover |

---

## Repository Structure

```
nist-csf-incident-response-playbook/
│
├── README.md
├── playbook/
│   ├── severity-table.md
│   ├── escalation-tree.md
│   ├── playbook-phishing.md
│   ├── playbook-brute-force.md
│   └── playbook-insider-threat.md
└── diagrams/
    └── escalation-flowchart.png
```

---

## NIST CSF Framework - Quick Reference

| Function | Purpose |
|----------|---------|
| **Identify** | Understand the scope and assets involved |
| **Protect** | Implement safeguards to limit impact |
| **Detect** | Identify occurrence of a security event |
| **Respond** | Take action on a detected incident |
| **Recover** | Restore capabilities after an incident |

---

## Severity Classification

| Level | SLA | Description |
|-------|-----|-------------|
| S4 - Low | 72 hrs | Minimal impact, likely false positive |
| S3 - Medium | 24 hrs | Isolated to one user/system, unconfirmed breach |
| S2 - High | 4 hrs | Active confirmed threat, multiple systems affected |
| S1 - Critical | 1 hr | Business disruption, data exfiltration likely |

Full table → [severity-table.md](playbook/severity-table.md)

---

## Skills Demonstrated

- Incident Response Lifecycle (Detection → Containment → Eradication → Recovery)
- NIST CSF Function Mapping
- Severity Classification and Triage
- Escalation Decision Making
- SOC Documentation and Process Design
- Threat Scenario Analysis (Phishing, Brute Force, Insider Threat)

---

## References

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CISA Incident Response Playbooks](https://www.cisa.gov/sites/default/files/publications/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf)
- [NIST SP 800-61 Rev. 2 - Computer Security Incident Handling Guide](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final)
