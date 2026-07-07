# SOC176 - RDP Brute Force Detected

## Alert Summary

An alert was triggered after multiple failed RDP authentication attempts were detected from a single source IP address against an internal host.

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | RDP Brute Force Detected |
| Severity | Medium |
| Source IP | 218.92.0.56 |
| Destination IP | 172.16.17.148 |
| Target Host | Matthew |
| Protocol | RDP |

---

## Initial Triage

The alert indicated repeated RDP authentication attempts against multiple accounts from the same external IP address.

Initial hypothesis:

> A brute-force attack may have been performed against the target host.

---

## Investigation Process

### Log Analysis

Investigated authentication events associated with source IP:

```
218.92.0.56
```

Observed multiple:

```
Event ID 4625
```

indicating failed logon attempts against several user accounts.

Examples:

- admin
- guest
- sysadmin
- Matthew

### Successful Authentication

Further analysis identified:

```
Event ID 4624
```

for user:

```
Matthew
```

originating from the same source IP:

```
218.92.0.56
```

This confirmed successful authentication.

---

### Endpoint Investigation

The compromised host was reviewed using Endpoint Security.

Observed activity included:

```
cmd.exe
whoami
net user letsdefend
net localgroup administrators
netstat -ano
```

---

### Post-Compromise Activity

The executed commands indicate discovery activity performed after successful authentication.

Examples:

#### User Discovery

```cmd
whoami
net user letsdefend
```

#### Privilege Discovery

```cmd
net localgroup administrators
```

#### Network Discovery

```cmd
netstat -ano
```

---

### Network Activity

Network connections between the compromised host and the source IP continued after successful authentication.

This is consistent with an active RDP session.

---

## Findings

- Multiple failed RDP authentication attempts were observed.
- A successful logon was identified.
- The same source IP was associated with both failed and successful logons.
- Discovery commands were executed after authentication.
- Post-compromise host activity was confirmed.

---

## MITRE ATT&CK Mapping

| Technique | ID |
|------------|------------|
| Brute Force | T1110 |
| Valid Accounts | T1078 |
| Account Discovery | T1087 |
| System Network Configuration Discovery | T1016 |

---

## Verdict

### True Positive

The investigation confirmed that the attacker successfully authenticated to the target host using valid credentials and subsequently performed discovery activities.

---

## Lessons Learned

- Always validate whether a brute-force attack resulted in successful authentication.
- Event ID 4624 and Event ID 4625 must be analyzed together.
- Timeline analysis is critical during authentication investigations.
- Post-compromise activity often provides stronger evidence than the original alert.
