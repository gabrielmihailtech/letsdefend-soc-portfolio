# SOC257 - VPN Connection Detected from Unauthorized Country

## Alert Summary

A VPN connection was detected from an unauthorized geographic location for user **monica@letsdefend.io**. The investigation focused on validating the connection source,
determining whether the activity was legitimate, and assessing the potential impact on the organization.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | VPN Connection Detected from Unauthorized Country |
| Severity | Medium |
| Event ID | 225 |
| Incident Type | Unauthorized Access |
| User | monica@letsdefend.io |
| Hostname | Monica |
| Host IP | 172.16.17.163 |
| Source IP | 113.161.158.12 |
| Destination IP | 33.33.33.33 |
| Destination Port | 443 |

---

## Initial Triage

The alert indicated that a VPN connection originated from a country that was not authorized for the user.

Initial objectives:

- Validate the source IP.
- Determine whether the user normally connects from that location.
- Assess whether the activity is malicious or legitimate.
- Identify potential impact to the environment.

---

## Threat Intelligence Analysis

The source IP address was investigated using Threat Intelligence.

### Source IP

```text
113.161.158.12
```

### Threat Intel Result

```text
Tag: Brute Force
Source: AbuseCH
```

The IP address had a known reputation associated with brute-force activity.

---

## Log Analysis

The VPN activity was reviewed through Log Management.

Observed:

```text
Source IP: 113.161.158.12
Destination Port: 443
Connection Type: Proxy / VPN
```

User activity associated with the account:

```text
monica@letsdefend.io
```

was reviewed for signs of suspicious behavior.

---

## User Activity Review

The account history was examined to determine whether the connection was consistent with normal user activity.

Findings:

- No previous evidence of VPN connections from the identified country.
- The user did not show a history of similar geographic access patterns.
- Browser activity appeared consistent with normal user browsing behavior.

Examples included:

```text
reddit.com
linkedin.com
bbc.com
youtube.com
wikipedia.org
instagram.com
```

---

## Endpoint Investigation

Host:

```text
Monica
(172.16.17.163)
```

was reviewed through Endpoint Security.

Observed activities included standard system and administrative commands.

Examples:

```text
systeminfo
ipconfig /all
netstat -ano
tasklist
driverquery
net user
wmic product get name
```

No malware artifacts or malicious processes were identified during the investigation.

---

## Findings

The investigation confirmed:

- VPN access originated from an unauthorized country.
- The source IP address was externally accessible.
- Threat Intelligence identified the IP as associated with brute-force activity.
- No prior history of connections from the same location was observed.
- No malware or additional indicators of compromise were identified on the endpoint.

---

## Indicators of Compromise (IOCs)

### Source IP Address

```text
113.161.158.12
```

### Destination Port

```text
443
```

### User Account

```text
monica@letsdefend.io
```

---

## Verdict

### True Positive

The investigation determined that the VPN connection originated from an unauthorized location and involved an externally sourced IP address with a known malicious reputation.

Although no malware activity was identified on the endpoint, the access pattern was inconsistent with the user's normal behavior and justified classification as an unauthorized access incident.

---

## Response Actions

- Investigated source IP reputation.
- Validated VPN activity.
- Reviewed endpoint activity.
- Reviewed browser history.
- Performed containment of the affected endpoint.
- Documented identified indicators.

---

## Lessons Learned

- VPN connections should always be validated against normal user behavior.
- Threat Intelligence can provide valuable context during authentication investigations.
- Geographic anomalies do not automatically indicate compromise but require investigation.
- Unauthorized access alerts should be correlated with endpoint and user activity before determining impact.
