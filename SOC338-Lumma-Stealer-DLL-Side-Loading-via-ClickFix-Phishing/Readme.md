# SOC338 - Lumma Stealer - DLL Side-Loading via ClickFix Phishing

## Alert Summary

A critical alert was generated after a phishing campaign delivered a ClickFix-style social engineering attack designed to distribute Lumma Stealer malware.

The investigation focused on validating the phishing email, determining whether the user interacted with the malicious content, identifying malicious execution activity, and assessing potential data theft risks.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | Lumma Stealer - DLL Side-Loading via ClickFix Phishing |
| Severity | Critical |
| Event ID | 316 |
| Alert Type | Data Leakage |
| Recipient | dylan@letsdefend.io |
| Sender | update@windows-update.site |
| SMTP Address | 132.232.40.201 |
| Email Subject | Upgrade your system to Windows 11 Pro for FREE |
| Device Action | Allowed |

---

## Initial Triage

The alert identified a phishing email associated with the distribution of Lumma Stealer through a ClickFix social engineering technique.

Initial objectives:

- Analyze the email contents.
- Determine whether the user accessed the malicious URL.
- Validate execution activity on the endpoint.
- Identify command execution and payload delivery mechanisms.
- Assess the risk of credential or data theft.

---

## Email Analysis

### Sender

```text
update@windows-update.site
```

### Recipient

```text
dylan@letsdefend.io
```

### Subject

```text
Upgrade your system to Windows 11 Pro for FREE
```

### Findings

The sender used a domain designed to appear related to Windows updates.

Observed malicious domain:

```text
windows-update.site
```

The email was delivered successfully:

```text
Device Action: Allowed
```

---

## User Interaction Analysis

Browser history confirmed that the recipient accessed the phishing website.

Observed URL:

```text
https://windows-update.site/
```

This confirmed that the recipient interacted with the phishing content.

---

## Endpoint Investigation

### Affected Host

```text
Hostname: Dylan
IP Address: 172.16.17.216
Operating System: Windows 10
```

---

## ClickFix Execution Evidence

Terminal history revealed PowerShell execution commands associated with a fake CAPTCHA verification page.

Observed command:

```text
I am not a robot - reCAPTCHA Verification
```

The phishing site instructed the user to execute commands which launched PowerShell and mshta.

Identified activity:

```powershell
PowerShell.exe
```

followed by:

```text
mshta.exe
```

fetching content from:

```text
https://overcoatpassably.shop/
```

and retrieving:

```text
maloy.mp4
```

The activity matched known ClickFix delivery techniques used to distribute Lumma Stealer.

---

## Network Activity Analysis

Network telemetry identified multiple outbound connections during the attack timeline.

Notable connection:

```text
132.232.40.201
```

Timestamp:

```text
2025-03-13 23:26:08
```

This IP matched infrastructure associated with the phishing alert.

Additional external connections were observed during payload execution.

---

## Attack Chain Reconstruction

```text
Phishing Email
        ↓
windows-update.site
        ↓
User Interaction
        ↓
Fake reCAPTCHA Verification
        ↓
PowerShell Execution
        ↓
mshta.exe
        ↓
overcoatpassably.shop
        ↓
Payload Retrieval
        ↓
Lumma Stealer Delivery
```

---

## Indicators of Compromise (IOCs)

### Sender Address

```text
update@windows-update.site
```

### Phishing Domain

```text
windows-update.site
```

### Payload Delivery Domain

```text
overcoatpassably.shop
```

### SMTP Infrastructure

```text
132.232.40.201
```

### Payload

```text
maloy.mp4
```

### LOLBin Used

```text
mshta.exe
```

---

## Findings Summary

The investigation confirmed:

- A phishing email was successfully delivered.
- The recipient accessed the phishing website.
- ClickFix social engineering techniques were used.
- PowerShell execution occurred on the endpoint.
- mshta.exe was used to retrieve remote content.
- Malicious infrastructure was contacted.
- Activity was consistent with Lumma Stealer delivery techniques.
- The incident posed a significant risk of credential theft and data exfiltration.

---

## Verdict

### True Positive

The alert accurately identified a Lumma Stealer delivery attempt through a ClickFix phishing campaign.

Evidence confirmed user interaction with the phishing site, PowerShell execution, mshta abuse, and communication with malicious infrastructure. The activity represented a confirmed malware delivery incident.

---

## Response Actions

- Investigated phishing email contents.
- Reviewed browser history.
- Validated user interaction.
- Analyzed PowerShell execution.
- Investigated mshta activity.
- Identified malicious domains and infrastructure.
- Contained the affected endpoint.
- Documented identified IOCs.

---

## Lessons Learned

- ClickFix campaigns continue to be highly effective against users through social engineering.
- Fake CAPTCHA verification pages can be used to convince users to execute malicious commands.
- PowerShell and mshta.exe are commonly abused during malware delivery.
- Browser history and endpoint telemetry are critical for validating user interaction.
- Early containment is essential when dealing with credential-stealing malware families such as Lumma Stealer.
