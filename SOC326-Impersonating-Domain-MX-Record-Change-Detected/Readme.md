# SOC326 - Impersonating Domain MX Record Change Detected

## Alert Summary

A phishing-related alert was generated after the detection of an impersonating domain configured with suspicious MX records.

The investigation focused on validating the reported domain, identifying potential phishing activity, determining whether the email reached the recipient, and verifying whether any user interaction occurred.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | Impersonating Domain MX Record Change Detected |
| Severity | High |
| Event ID | 304 |
| Sender | no-reply@cti-report.io |
| Recipient | soc@letsdefend.io |
| Date | Sep 17, 2024 |
| Email Action | Allowed |

---

## Initial Triage

The alert indicated the existence of a domain impersonating the legitimate LetsDefend domain.

Initial objectives:

- Identify the impersonating domain.
- Validate whether the domain was malicious.
- Determine whether the notification email was delivered.
- Check for any user interaction with the phishing infrastructure.
- Assess organizational impact.

---

## Email Analysis

The notification email reported a newly identified impersonating domain.

### Sender

```text
no-reply@cti-report.io
```

### Recipient

```text
soc@letsdefend.io
```

### Subject

```text
Impersonating Domain MX Record Change Detected
```

### Email Status

```text
Allowed
```

This confirmed successful delivery of the email.

---

## Domain Investigation

The investigation identified the following suspicious domain:

```text
letsdefwnd.io
```

The domain appears designed to impersonate:

```text
letsdefend.io
```

by replacing the letter:

```text
e
```

with:

```text
w
```

This technique is commonly known as typo-squatting and is frequently used in phishing campaigns.

---

## Threat Intelligence Analysis

The identified domain was investigated using Threat Intelligence.

### Domain

```text
letsdefwnd.io
```

### Threat Intelligence Result

```text
Tag: phishing
```

This confirmed that the domain had already been identified as phishing infrastructure.

---

## DNS and MX Record Information

Observed MX Record:

```text
mail.mailerhost.net
```

Additional details collected during the investigation:

```text
Incident Main Type: Brand Protection
Incident Sub Type: Impersonating Domain
Risk Level: High
```

The impersonating domain was configured to receive email traffic, increasing the likelihood of phishing activity.

---

## Log Analysis

Log Management was used to determine whether the phishing domain had been accessed by the email recipient.

### Findings

Email delivery was confirmed through Exchange logs.

Observed fields:

```text
Sender: no-reply@cti-report.io
Recipient: soc@letsdefend.io
Destination Port: 25
```

---

### User Interaction Review

Additional searches were performed for:

```text
letsdefwnd.io
```

Log analysis identified access attempts from another user account within the environment:

```text
User: Mateo
URL: https://letsdefwnd.io
```

However, no evidence was found linking the recipient of this alert:

```text
soc@letsdefend.io
```

to any interaction with the phishing domain.

---

## Indicators of Compromise (IOCs)

### Phishing Domain

```text
letsdefwnd.io
```

### Sender Address

```text
no-reply@cti-report.io
```

### MX Record

```text
mail.mailerhost.net
```

---

## Findings Summary

The investigation determined that:

- A typo-squatting domain impersonating LetsDefend was identified.
- Threat Intelligence classified the domain as phishing.
- The notification email was successfully delivered.
- MX records were configured for the impersonating domain.
- No evidence was found showing interaction by the email recipient.
- Phishing infrastructure was identified and documented.

---

## Verdict

### True Positive

The alert accurately identified a phishing-related domain impersonation event.

Threat Intelligence confirmed the domain as phishing infrastructure and the domain was configured to receive email traffic through active MX records.

Although no interaction by the intended recipient was identified, the domain represented a legitimate phishing risk to the organization.

---

## Response Actions

- Investigated the phishing domain.
- Reviewed MX record configuration.
- Validated threat intelligence results.
- Checked email delivery status.
- Reviewed logs for user interaction.
- Removed the email from the recipient mailbox.
- Performed containment actions as required by the response process.

---

## Lessons Learned

- Typosquatting domains are commonly used to impersonate trusted organizations.
- MX record monitoring can provide early visibility into phishing infrastructure.
- Threat Intelligence can quickly validate suspicious domains.
- Email delivery should be verified separately from user interaction.
- Domain impersonation alerts should be investigated even when no user interaction is observed.
