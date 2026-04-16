# Playbook 1 — Phishing Attack

## What is a Phishing Attack?

A phishing attack is a social engineering attempt where an attacker sends a fraudulent email (or message) disguised as a legitimate source to trick a user into revealing credentials, clicking a malicious link, or downloading malware.

**Common variants:**
- Spear phishing — targeted at a specific individual
- Whaling — targeted at executives
- Smishing — phishing via SMS

---

## How It Is Detected

| Detection Source | Signal |
|-----------------|--------|
| Email security gateway (e.g. Proofpoint, Mimecast) | Flags suspicious sender domain, spoofed headers |
| User report | Employee forwards suspicious email to security team |
| SIEM alert | Detects mass email with identical subject line |
| Endpoint alert | Antivirus flags downloaded attachment |
| Threat intelligence feed | Known phishing domain or IP flagged |

---

## Severity Classification

| Condition | Severity |
|-----------|----------|
| Phishing email received, not opened | 🟢 Low (S4) |
| Email opened, no link clicked | 🟢 Low (S4) |
| Link clicked, no credentials entered | 🟡 Medium (S3) |
| Credentials entered on phishing page | 🟠 High (S2) |
| Credential used + lateral movement detected | 🔴 Critical (S1) |

Refer to [Severity Classification Table](severity-table.md) for SLAs and notification requirements.

---

## NIST CSF Response Steps

### 🔵 IDENTIFY
> Understand the scope — who and what is affected.

- [ ] Identify the affected user(s) who received or clicked the phishing email
- [ ] Retrieve the original phishing email (headers, sender, links, attachments)
- [ ] Identify all recipients of the same phishing campaign using email gateway logs
- [ ] Determine if any attachments were downloaded or links were clicked
- [ ] Check if the phishing domain/IP is in threat intelligence feeds
- [ ] Identify what systems the affected user has access to

**Key questions to answer:**
- How many users received this email?
- Was any link clicked or attachment opened?
- What credentials or data could be at risk?

---

### 🟢 PROTECT
> Prevent further damage while investigation continues.

- [ ] Block the phishing sender domain and IP at the email gateway
- [ ] Add the malicious URL to the web proxy blocklist
- [ ] Remove the phishing email from all inboxes (quarantine/delete)
- [ ] If credentials were entered — force password reset immediately
- [ ] If credentials were entered — revoke all active sessions for affected account
- [ ] Enable or confirm MFA is active on affected account
- [ ] Notify all users who received the email with a warning not to click

---

### 🟡 DETECT
> Determine the full extent of the compromise.

- [ ] Search email logs for all recipients of the phishing campaign
- [ ] Check web proxy/firewall logs for connections to the phishing domain
- [ ] Review authentication logs for the affected user — look for logins from unusual IPs or locations
- [ ] Check for any email forwarding rules added to the compromised account
- [ ] Check for any new inbox rules (attackers often create auto-delete or forward rules)
- [ ] Search endpoint logs for any downloaded malware or script execution
- [ ] Run IOC (Indicator of Compromise) search across SIEM for phishing domain and sender IP

**IOCs to search for:**
- Phishing domain name
- Sender email address and IP
- URLs embedded in the email
- File hash of any attachment

---

### 🔴 RESPOND
> Take action to contain and eliminate the threat.

- [ ] Isolate the affected endpoint if malware was executed
- [ ] Lock the compromised account if credential misuse is confirmed
- [ ] Escalate to Tier 2 / SOC Manager per [Escalation Decision Tree](escalation-tree.md)
- [ ] Notify HR and Legal if sensitive data was accessed
- [ ] Preserve evidence — export logs, email headers, proxy records before any remediation
- [ ] Submit phishing URL and email to threat intelligence platform (e.g. VirusTotal, PhishTank)
- [ ] Report phishing domain for takedown (ICANN, hosting provider abuse contact)
- [ ] Interview the affected user to understand exactly what actions were taken

**Containment decision:**
- Credential entered → immediate forced password reset + session revoke
- Malware executed → isolate endpoint, image for forensics before wiping
- No click → monitoring only, educate user

---

### 🟣 RECOVER
> Restore normal operations securely.

- [ ] Confirm malicious email has been removed from all inboxes
- [ ] Confirm phishing domain/IP is blocked across all controls (email, proxy, firewall)
- [ ] Restore access to affected user after password reset and MFA confirmation
- [ ] Restore or re-image endpoint if malware was confirmed
- [ ] Monitor affected account for 30 days for anomalous activity
- [ ] Send phishing awareness reminder to all staff
- [ ] Update email gateway rules and blocklists based on this campaign
- [ ] Close the incident ticket with full timeline documentation

---

## Lessons Learned Checklist

After incident closure, review the following:

- [ ] How did the phishing email bypass existing controls?
- [ ] Was the email flagged by any existing tool — if not, why not?
- [ ] How quickly did the user report the email?
- [ ] Should email gateway rules be updated?
- [ ] Should phishing simulation training be scheduled?
- [ ] Were all playbook steps followed — any gaps?
- [ ] Update this playbook if any steps were missing or unclear

---

## NIST CSF Function Summary

| NIST Function | Actions Taken |
|--------------|--------------|
| Identify | Scope affected users, analyze email, check threat intel |
| Protect | Block domain/IP, remove email, reset credentials, enforce MFA |
| Detect | Search logs, review auth events, hunt for IOCs in SIEM |
| Respond | Isolate endpoint, lock account, preserve evidence, report domain |
| Recover | Restore access, monitor account, update controls, staff training |

---

## Related Documents

- [Severity Classification Table](severity-table.md)
- [Escalation Decision Tree](escalation-tree.md)
