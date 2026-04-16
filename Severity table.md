# Severity Classification Table

This table is referenced by all playbooks to classify incidents and determine response SLAs and escalation paths.

---

## Severity Levels

| Level | Name | SLA (Response Time) | Description | Example Scenarios | Who to Notify |
|-------|------|-------------------|-------------|-------------------|---------------|
| **S1** | Critical | 1 hour | Severe impact. Business operations disrupted. Data exfiltration likely or confirmed. | Ransomware deployed, confirmed insider data theft, C2 communication detected, mass credential compromise | SOC Manager + CISO + Legal + Executive Team |
| **S2** | High | 4 hours | Significant impact. Active threat confirmed. Multiple systems or users affected. | Credentials stolen and used, brute force succeeding, malware executing, privilege escalation confirmed | Tier 2 Analyst + SOC Manager |
| **S3** | Medium | 24 hours | Limited impact. Isolated to one user or system. No confirmed breach yet. | Phishing email clicked but no credentials entered, port scan detected, single failed MFA | Tier 1 → Tier 2 escalation |
| **S4** | Low | 72 hours | Minimal impact. No data loss. Likely a false positive or minor policy violation. | Single failed login, spam email flagged by filter, benign suspicious URL reported | Tier 1 analyst only |

---

## How to Use This Table

1. When an alert is received, read the description column and match it to the closest scenario.
2. Note the **SLA** — this is the maximum time before your first response action must be taken.
3. Follow the **Who to Notify** column immediately — do not wait until after investigation to escalate.
4. Document your severity decision with justification in your incident ticket.

---

## Severity Escalation Rule

> If at any point during investigation the severity appears **higher** than initially classified, **escalate immediately** — do not wait for confirmation.

It is always better to over-escalate and downgrade later than to under-escalate and miss the response window.

---

## Related Documents

- [Escalation Decision Tree](escalation-tree.md)
- [Phishing Playbook](playbook-phishing.md)
- [Brute Force Playbook](playbook-brute-force.md)
- [Insider Threat Playbook](playbook-insider-threat.md)
