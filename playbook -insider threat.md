# Playbook 3 — Insider Threat

## What is an Insider Threat?

An insider threat is a security risk that originates from within the organization — typically a current or former employee, contractor, or business partner who misuses their authorized access to harm the organization, whether intentionally or unintentionally.

**Common variants:**
- Malicious insider — deliberate data theft, sabotage, or fraud
- Negligent insider — accidental data exposure, policy violations, falling for phishing
- Compromised insider — legitimate account taken over by an external attacker

---

## How It Is Detected

| Detection Source | Signal |
|-----------------|--------|
| DLP (Data Loss Prevention) tool | Bulk download or upload of sensitive files |
| SIEM alert | Access to resources outside normal working hours or unusual locations |
| User Behavior Analytics (UBA) | Deviation from baseline behavior — sudden spike in file access |
| HR / Manager report | Employee displaying behavioral red flags (resignation, grievance, financial stress) |
| Email gateway | Sensitive documents emailed to personal email address |
| Audit logs | Access to data outside the user's role or department |

---

## Severity Classification

| Condition | Severity |
|-----------|----------|
| Minor policy violation, no data loss (e.g. accessing a restricted folder once) | 🟢 Low (S4) |
| Repeated policy violations or suspicious access pattern | 🟡 Medium (S3) |
| Confirmed unauthorized access to sensitive data | 🟠 High (S2) |
| Data exfiltration confirmed or sabotage detected | 🔴 Critical (S1) |

Refer to [Severity Classification Table](severity-table.md) for SLAs and notification requirements.

---

## ⚠️ Special Handling Notice

> Insider threat investigations are **sensitive and legally complex**. HR and Legal must be involved from the moment the threat is confirmed as **High or Critical**. Do not confront or notify the subject of the investigation until HR and Legal provide clearance. Premature disclosure can result in evidence destruction or legal liability.

---

## NIST CSF Response Steps

### 🔵 IDENTIFY
> Understand who is involved and what data or systems are at risk.

- [ ] Identify the user account involved and their role in the organization
- [ ] Determine what data, systems, or assets were accessed or potentially compromised
- [ ] Review the user's access permissions — do they legitimately have access to what they accessed?
- [ ] Establish a baseline of the user's normal behavior from historical logs
- [ ] Identify whether the user is currently employed or recently departed
- [ ] Determine if this is a malicious, negligent, or compromised insider scenario
- [ ] Coordinate with HR to understand if there are any behavioral red flags or recent employment changes

**Key questions to answer:**
- Is the access pattern a genuine anomaly or within normal variation?
- What is the business sensitivity of the data accessed?
- Is the user aware they are being investigated?

---

### 🟢 PROTECT
> Minimize further data exposure without alerting the subject prematurely.

- [ ] Do NOT lock or disable the account immediately — this alerts the insider (consult HR/Legal first)
- [ ] Silently increase logging and monitoring on the account
- [ ] Implement a DLP rule to block further data transfers from this user if not already in place
- [ ] Revoke any elevated privileges that are not essential to the user's current work
- [ ] Alert the user's system owner and data owners without informing the subject
- [ ] Confirm data backup integrity of any systems the user has write access to
- [ ] Restrict remote access (VPN) if data exfiltration is confirmed and HR/Legal approve

---

### 🟡 DETECT
> Build a full picture of what happened.

- [ ] Pull all access logs for the user for the past 30–90 days
- [ ] Review DLP logs for file transfers, USB activity, email attachments, and cloud uploads
- [ ] Check email logs for forwarding to personal addresses or unusual recipients
- [ ] Review authentication logs — after-hours access, access from home or unusual locations
- [ ] Search SIEM for all systems the user has touched — map access timeline
- [ ] Check for use of personal cloud storage tools (Dropbox, Google Drive) from corporate devices
- [ ] Review printer logs and USB device connection logs
- [ ] Identify if any colleagues' credentials were used by or shared with the subject

**Evidence to collect:**
- SIEM access timeline (user + affected systems)
- DLP event logs
- Email metadata (sender, recipient, attachment names, timestamps)
- File audit logs (which files were accessed, copied, moved, or deleted)

---

### 🔴 RESPOND
> Contain the threat while preserving evidence and following legal process.

- [ ] Escalate to SOC Manager, CISO, HR, and Legal per [Escalation Decision Tree](escalation-tree.md)
- [ ] Preserve all digital evidence — do not alter logs, do not wipe systems
- [ ] Work with Legal to understand data breach notification obligations
- [ ] Work with HR on the formal employee investigation process
- [ ] Once HR/Legal approve — disable user account, revoke all access (including VPN, SSO, SaaS apps)
- [ ] Recover or identify any data that was exfiltrated — determine if it is recoverable
- [ ] If sabotage detected — isolate affected systems, assess damage, initiate system recovery
- [ ] Coordinate with Law Enforcement if criminal activity is confirmed (e.g. IP theft, fraud)

**Containment decision:**
- Negligent insider → educate, remediate data exposure, policy enforcement
- Malicious insider → full account lockout (HR/Legal approved), legal proceedings
- Compromised insider → treat as external breach — isolate account, investigate attacker

---

### 🟣 RECOVER
> Restore trust and secure operations after the incident.

- [ ] Revoke all access for the former insider across all systems and third-party apps
- [ ] Audit all systems and data the insider had access to for tampering or backdoors
- [ ] Recover or contain any exfiltrated data (legal hold, notification to affected parties)
- [ ] Review and update access control policies — enforce least privilege
- [ ] Review offboarding procedures — were they followed correctly?
- [ ] Conduct access review for all high-risk users (those with elevated privileges)
- [ ] Update DLP and UBA rules based on techniques used in this incident
- [ ] Provide findings to HR and Legal for any disciplinary or legal action
- [ ] Close the incident ticket with full timeline and documentation

---

## Lessons Learned Checklist

After incident closure, review the following:

- [ ] Were access controls following least privilege? Did the user have more access than needed?
- [ ] How long was the activity occurring before detection?
- [ ] Were there behavioral signals that were missed (HR friction, policy violations)?
- [ ] Was the offboarding process adequate for departed employees?
- [ ] Should UBA baselines or DLP thresholds be adjusted?
- [ ] Was HR and Legal notified at the right time in the process?
- [ ] Update this playbook if any steps were missing or unclear

---

## NIST CSF Function Summary

| NIST Function | Actions Taken |
|--------------|--------------|
| Identify | Identify user, access scope, data sensitivity, insider type |
| Protect | Increase monitoring, restrict privileges, DLP rules (without alerting subject) |
| Detect | Pull access logs, DLP events, email metadata, build full activity timeline |
| Respond | Escalate to HR/Legal, preserve evidence, disable account on approval |
| Recover | Revoke all access, audit systems, update access controls, policy review |

---

## Related Documents

- [Severity Classification Table](severity-table.md)
- [Escalation Decision Tree](escalation-tree.md)
