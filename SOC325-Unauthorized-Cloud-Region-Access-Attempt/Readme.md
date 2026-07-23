# SOC325 - Unauthorized Cloud Region Access Attempt

## Alert Summary

A cloud security alert was generated after multiple login attempts were detected from an unauthorized cloud region.

The investigation focused on identifying the source of the activity, determining whether the authentication attempts were successful, evaluating potential defense evasion techniques, and assessing the impact on the targeted cloud service.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | Unauthorized Cloud Region Access Attempt Detected |
| Severity | Low |
| Event ID | 303 |
| Incident Type | Web Attack |
| Source IP | 134.209.145.73 |
| Destination IP | 52.15.206.21 |
| Username | test@letsdefend.io |
| Request URL | POST /accounts/login |
| Action | Blocked |

---

## Initial Triage

The alert indicated multiple authentication attempts originating from an unauthorized cloud region against a cloud-hosted application.

Initial objectives:

- Identify the source of the activity.
- Determine whether the attempts were successful.
- Investigate potential defense evasion techniques.
- Evaluate the scope and impact of the activity.
- Determine whether containment actions were necessary.

---

## Investigation

### Alert Review

The alert details revealed:

```text
Source IP: 134.209.145.73
Destination IP: 52.15.206.21
Username: test@letsdefend.io
```

Observed request:

```text
POST /accounts/login
```

Security controls generated the following message:

```text
Suspicious activity from unused cloud region detected,
connection blocked
```

---

### Authentication Activity

The alert indicated:

```text
Multiple login attempts
```

targeting:

```text
test@letsdefend.io
```

The requests originated from a cloud region that was configured as unauthorized or unused by the organization.

Observed response:

```text
HTTP 403
Access Denied
```

Device Action:

```text
Blocked
```

This indicated that the authentication attempts were prevented before successful access could be established.

---

### Endpoint Investigation

Endpoint Security was reviewed for the affected system.

Host:

```text
AWS_Services
```

System Information:

```text
Operating System: Ubuntu 20.04.02
Server Type: Linux Server
```

---

### Browser Activity Review

Browser history showed visits to legitimate Linux and operating system-related websites, including:

```text
archlinux.org
linux.org
ubuntu.com
linuxmint.com
linuxfoundation.org
centos.org
redhat.com
debian.org
suse.com
fedora.org
```

No suspicious browsing activity was identified.

---

### Terminal Activity Review

Terminal history contained normal Ubuntu and system administration processes.

Examples included:

```text
cron.daily
cloud-init
systemd
apt.systemd.daily
update-notifier
```

No suspicious commands, malware execution, persistence mechanisms, or unauthorized administrative actions were observed.

---

### Network Review

Network activity was reviewed following the alert.

The observed connections occurred after the blocked login attempts and appeared consistent with normal server operations.

No evidence of command-and-control traffic, malware communication, or successful compromise was identified.

---

## Defense Evasion Analysis

The alert specifically identified activity originating from an unauthorized cloud region.

Observed technique:

```text
Unused / Unsupported Cloud Regions
```

This behavior aligns with attempts to bypass security monitoring and access controls by originating traffic from a cloud region not normally used by the organization.

---

## Indicators of Compromise (IOCs)

### Source IP

```text
134.209.145.73
```

### Target User

```text
test@letsdefend.io
```

### Destination Server

```text
52.15.206.21
```

### Login Endpoint

```text
POST /accounts/login
```

---

## Findings Summary

The investigation determined that:

- Multiple authentication attempts targeted test@letsdefend.io.
- The activity originated from an unauthorized cloud region.
- Login requests were directed at the application's authentication endpoint.
- Security controls blocked the activity.
- Access was denied through HTTP 403 responses.
- No evidence of successful authentication was identified.
- No malware, persistence, or post-compromise activity was observed.
- The activity was limited to a single source IP and a single target system.

---

## Verdict

### True Positive

The alert correctly identified suspicious authentication activity originating from an unauthorized cloud region.

Although the activity represented a genuine attack attempt, security controls successfully blocked the requests and prevented unauthorized access.

---

## Response Actions

- Investigated source and destination IP addresses.
- Reviewed authentication activity.
- Evaluated defense evasion techniques.
- Reviewed endpoint activity.
- Reviewed browser and terminal history.
- Assessed network activity.
- Confirmed that access attempts were blocked.

---

## Lessons Learned

- Cloud region monitoring provides valuable visibility into abnormal authentication activity.
- Attack attempts may be detected through behavioral analysis even when threat intelligence data is unavailable.
- Unauthorized cloud regions can be leveraged as a defense evasion technique.
- A blocked attack should still be classified as a True Positive when malicious behavior is confirmed.
- Successful detection and prevention reduce the likelihood of compromise and limit the incident scope.
