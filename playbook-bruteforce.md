# Playbook 2 — Brute Force Attack

## What is a Brute Force Attack?

A brute force attack is an attempt to gain unauthorized access to a system by systematically trying a large number of username and password combinations until the correct one is found.

**Common variants:**
- Classic brute force — trying all possible combinations
- Dictionary attack — using a wordlist of common passwords
- Credential stuffing — using previously leaked username/password pairs from data breaches
- Password spraying — trying one common password across many accounts (avoids lockouts)

---

## How It Is Detected

| Detection Source | Signal |
|-----------------|--------|
| SIEM alert | Multiple failed login attempts from a single IP in a short time window |
| Authentication logs | Account lockout triggered, or threshold of failed logins reached |
| IDS/IPS | Detects scanning or login attempt patterns |
| Threat intelligence | Source IP flagged as known attacker or TOR exit node |
| User report | User reports being locked out without attempting to log in |

**Typical SIEM rule:** 5+ failed login attempts within 5 minutes from the same source IP = alert.

---

## Severity Classification

| Condition | Severity |
|-----------|----------|
| Failed attempts against one account, no lockout | 🟢 Low (S4) |
| Account locked out from repeated attempts | 🟡 Medium (S3) |
| Multiple accounts targeted simultaneously | 🟠 High (S2) |
| Successful login after brute force attempts | 🟠 High (S2) |
| Successful login + lateral movement or privilege escalation | 🔴 Critical (S1) |

Refer to [Severity Classification Table](severity-table.md) for SLAs and notification requirements.

---

## NIST CSF Response Steps

### 🔵 IDENTIFY
> Understand the scope — who and what is being targeted.

- [ ] Identify the targeted account(s) and system(s)
- [ ] Determine the source IP address(es) of the attack
- [ ] Check threat intelligence feeds to identify if the source IP is a known attacker
- [ ] Identify whether this is a targeted attack or a broad spray across multiple accounts
- [ ] Determine the time window and total number of attempts
- [ ] Check if the targeted account has admin or privileged access
- [ ] Identify whether any login attempt succeeded

**Key questions to answer:**
- Is this credential stuffing (using real leaked creds) or random guessing?
- Did any attempt succeed?
- Is the target account a standard user or privileged/admin account?

---

### 🟢 PROTECT
> Limit the attacker's ability to continue or escalate.

- [ ] Block the source IP at the firewall immediately
- [ ] If attack is distributed (many IPs) — consider geo-blocking or rate limiting
- [ ] Lock the targeted account(s) if not already auto-locked
- [ ] Force password reset on targeted account(s) as a precaution
- [ ] Verify MFA is enabled on all targeted accounts — if not, enforce immediately
- [ ] Ensure account lockout policy is active (e.g., lock after 5 failed attempts)
- [ ] Temporarily disable externally exposed login pages if attack is ongoing

---

### 🟡 DETECT
> Determine if any attempt was successful.

- [ ] Review authentication logs for successful logins from the attacking IP or unusual locations
- [ ] Check for logins occurring after the brute force attempts (possible successful guess)
- [ ] Search SIEM for the attacking IP across all log sources — not just the targeted system
- [ ] Look for lateral movement: did the attacker access other systems after successful login?
- [ ] Check for privilege escalation attempts post-login
- [ ] Review VPN and remote access logs for the targeted account
- [ ] Check if any new accounts were created or permissions changed during the attack window

**IOCs to search for:**
- Attacking IP address(es)
- Targeted username(s)
- Time window of attack
- User-agent strings used during login attempts

---

### 🔴 RESPOND
> Contain the threat and eradicate unauthorized access.

- [ ] If login was successful — immediately revoke all active sessions for the compromised account
- [ ] Lock the compromised account pending investigation
- [ ] Escalate per [Escalation Decision Tree](escalation-tree.md) if login was confirmed successful
- [ ] Preserve authentication logs and SIEM data before any changes
- [ ] If lateral movement detected — isolate affected systems immediately
- [ ] Notify the account owner to confirm whether they initiated any of the login attempts
- [ ] Report attacking IP to threat intelligence platform (e.g. AbuseIPDB)
- [ ] Review whether password policy meets minimum complexity requirements

**Containment decision:**
- No successful login → block IP, monitor, educate user on strong passwords
- Successful login, no lateral movement → revoke sessions, reset password, MFA enforcement
- Successful login + lateral movement → incident escalation to S1, isolate systems

---

### 🟣 RECOVER
> Restore access and harden against future attacks.

- [ ] Restore account access after verified password reset and MFA activation
- [ ] Remove attacker IP blocks only after confirmed attack has stopped
- [ ] Audit all actions taken on the compromised account during the attack window
- [ ] Review and tighten account lockout and password policies if gaps found
- [ ] Verify no persistence mechanisms were installed (scheduled tasks, new accounts, backdoors)
- [ ] Monitor the previously targeted account for 30 days
- [ ] Update SIEM detection rules if the attack pattern was not caught initially
- [ ] Close incident ticket with full timeline and root cause documentation

---

## Lessons Learned Checklist

After incident closure, review the following:

- [ ] How long did the attack run before detection? Is the SIEM alert threshold appropriate?
- [ ] Was the lockout policy effective — did it trigger correctly?
- [ ] Was MFA in place on the targeted account? If not, why not?
- [ ] Was the attacking IP from a known malicious source — was it already in a blocklist?
- [ ] Did credential stuffing succeed because of a password reuse issue?
- [ ] Should the detection threshold be adjusted?
- [ ] Update this playbook if any steps were missing or unclear

---

## NIST CSF Function Summary

| NIST Function | Actions Taken |
|--------------|--------------|
| Identify | Identify targeted accounts, source IPs, attack type, and scope |
| Protect | Block IPs, lock accounts, enforce MFA, apply rate limiting |
| Detect | Review auth logs for successful logins, hunt for lateral movement |
| Respond | Revoke sessions, isolate systems, preserve logs, escalate |
| Recover | Restore access, audit account activity, harden policy, monitor |

---

## Related Documents

- [Severity Classification Table](severity-table.md)
- [Escalation Decision Tree](escalation-tree.md)
