# SOC282 - Phishing Alert - Deceptive Mail Detected

## Alert Summary

A phishing alert was generated after a suspicious email containing a URL and a password-protected ZIP attachment was delivered to a user mailbox.

The investigation focused on determining whether the email was malicious, whether the recipient interacted with it, and whether any malicious payload execution occurred.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | Phishing Alert - Deceptive Mail Detected |
| Severity | Medium |
| Event ID | 257 |
| Sender | free@coffeeshooop.com |
| Recipient | Felix@letsdefend.io |
| Subject | Free Coffee Voucher |
| Source IP | 103.60.134.63 |
| Email Action | Allowed |

---

## Initial Triage

The alert identified a potentially deceptive email sent to an internal user.

Initial objectives:

- Review the email contents.
- Identify URLs or attachments.
- Determine whether the email was delivered.
- Determine whether the user interacted with the email.
- Assess potential impact.

---

## Email Analysis

The email promoted a free coffee voucher and attempted to entice the recipient to click a link.

### Subject

```
Free Coffee Voucher
```

### Sender

```
free@coffeeshooop.com
```

### Recipient

```
Felix@letsdefend.io
```

### Observations

The sender domain appeared suspicious due to possible typosquatting:

```
coffeeshooop.com
```

The email contained both a clickable URL and a password-protected ZIP attachment.

---

## Attachment Analysis

Observed attachment:

```
free-coffee.zip
```

Attachment password:

```
infected
```

The use of password-protected archives is a common technique used to avoid email security scanning.

---

## URL Analysis

The email included a button labeled:

```
Redeem Now
```

Log analysis later confirmed access to the associated URL.

Observed download URL:

```
https://files-ld.s3.us-east-2.amazonaws.com/59cbd215-76ea-434d-93ca-4d6aec3bac98-free-coffee.zip
```

---

## Log Analysis

Log Management was used to determine whether the recipient interacted with the email.

### Findings

User:

```
Felix
```

accessed the URL through:

```
chrome.exe
```

Observed event:

```
Device Action: Allowed
```

URL:

```
https://files-ld.s3.us-east-2.amazonaws.com/.../free-coffee.zip
```

This confirmed that the recipient clicked the phishing content and accessed the hosted ZIP file.

---

## Investigation Findings

The following attack chain was identified:

```
Phishing Email Delivered
           ↓
User Opens Email
           ↓
User Clicks URL
           ↓
Chrome Accesses Hosted ZIP File
           ↓
free-coffee.zip Downloaded / Accessed
```

No evidence was identified indicating that the downloaded payload was executed.

---

## Indicators of Compromise (IOCs)

### Sender Email

```
free@coffeeshooop.com
```

### Sender Domain

```
coffeeshooop.com
```

### Source IP

```
103.60.134.63
```

### Attachment

```
free-coffee.zip
```

### Download URL

```
https://files-ld.s3.us-east-2.amazonaws.com/59cbd215-76ea-434d-93ca-4d6aec3bac98-free-coffee.zip
```

---

## Findings Summary

- The email contained both a URL and an attachment.
- The email was successfully delivered to the recipient.
- The sender domain appeared suspicious.
- The recipient accessed the malicious content.
- The ZIP file was downloaded or accessed through Chrome.
- No evidence of payload execution was identified during the investigation.

---

## Verdict

### True Positive

The alert was confirmed as a phishing incident.

The email contained suspicious content, a deceptive sender domain, and a downloadable ZIP attachment. Log analysis confirmed user interaction with the phishing content.

---

## Response Actions

- Investigated email content.
- Identified suspicious sender domain.
- Validated attachment and URL presence.
- Confirmed user interaction through log analysis.
- Removed malicious email from the recipient mailbox.
- Contained the affected endpoint as a precautionary measure.

---

## Lessons Learned

- Typosquatting domains are commonly used in phishing campaigns.
- Password-protected ZIP files should be treated as high-risk attachments.
- User interaction with phishing content must always be verified through logs.
- Download activity does not automatically indicate payload execution.
- Email alerts should be correlated with endpoint and network activity to determine impact.
