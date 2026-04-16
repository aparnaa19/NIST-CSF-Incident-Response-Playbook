# Escalation Decision Tree

Use this tree for every incoming alert to determine whether to escalate and to whom.

---

## Decision Tree

```
ALERT RECEIVED
│
├──► Is this a confirmed active threat?
│         │
│         ├── YES ──► Are multiple systems or users affected?
│         │                   │
│         │                   ├── YES ──► Is data exfiltration confirmed or likely?
│         │                   │                   │
│         │                   │                   ├── YES ──► 🔴 CRITICAL (S1)
│         │                   │                   │           Notify: SOC Manager + CISO + Legal
│         │                   │                   │           SLA: 1 hour
│         │                   │                   │
│         │                   │                   └── NO  ──► 🟠 HIGH (S2)
│         │                   │                               Notify: Tier 2 + SOC Manager
│         │                   │                               SLA: 4 hours
│         │                   │
│         │                   └── NO  ──► 🟠 HIGH (S2)
│         │                               Notify: Tier 2 + SOC Manager
│         │                               SLA: 4 hours
│         │
│         └── NO  ──► Is there suspicious activity with no confirmed breach?
│                             │
│                             ├── YES ──► 🟡 MEDIUM (S3)
│                             │           Notify: Escalate Tier 1 → Tier 2
│                             │           SLA: 24 hours
│                             │
│                             └── NO  ──► Is this likely a false positive or minor violation?
│                                                 │
│                                                 ├── YES ──► 🟢 LOW (S4)
│                                                 │           Notify: Tier 1 analyst only
│                                                 │           SLA: 72 hours
│                                                 │
│                                                 └── NO  ──► Re-investigate and re-classify
```

---

## Escalation Contacts

| Role | When to Contact | Responsibility |
|------|----------------|----------------|
| **Tier 1 Analyst** | All incidents | Initial triage, log collection, basic containment |
| **Tier 2 Analyst** | S2 and above | Deep investigation, root cause analysis |
| **SOC Manager** | S2 and above | Oversight, resource allocation, stakeholder updates |
| **CISO** | S1 only | Executive decision making, regulatory obligations |
| **Legal / Compliance** | S1 only | Data breach notification, regulatory reporting |
| **IT / System Owners** | As needed | System isolation, account lockout, restoration |
| **HR** | Insider threat cases | Employee investigation, disciplinary process |

---

## Escalation Rules

1. **Never delay escalation** waiting for full investigation — escalate based on available evidence.
2. **Communicate verbally first** for S1/S2 — do not rely on email alone.
3. **Document every escalation** — who was notified, when, and what information was shared.
4. **Downgrade is allowed** — if investigation reveals lower severity, document the reason and inform all notified parties.
5. **Re-escalate if needed** — if new evidence raises severity during investigation, escalate again immediately.

---

## Related Documents

- [Severity Classification Table](severity-table.md)
- [Phishing Playbook](playbook-phishing.md)
- [Brute Force Playbook](playbook-brute-force.md)
- [Insider Threat Playbook](playbook-insider-threat.md)
