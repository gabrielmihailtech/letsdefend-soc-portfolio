# SOC342 - SharePoint ToolShell Authentication Bypass and Remote Code Execution

## Alert Summary

A critical alert was generated after suspicious activity associated with SharePoint ToolShell exploitation was detected.

The investigation identified unauthorized payload delivery, compilation of malicious code, PowerShell abuse, and execution activity consistent with remote code execution on a SharePoint server.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | SharePoint ToolShell Auth Bypass and RCE |
| Severity | Critical |
| Hostname | SharePoint01 |
| Host IP | 172.16.20.171 |
| Alert Type | Web Application Exploitation |
| Technique | Authentication Bypass / Remote Code Execution |

---

## Initial Triage

The alert indicated potential exploitation of a SharePoint server through a ToolShell-style attack.

Initial objectives:

- Validate exploitation activity.
- Identify malicious payloads.
- Determine whether code execution occurred.
- Identify attacker infrastructure.
- Assess the impact on the SharePoint server.

---

## Endpoint Investigation

### Affected Host

```text
Hostname: SharePoint01
IP Address: 172.16.20.171
```

The endpoint investigation focused on terminal activity, payload execution, and generated files.

---

## Terminal History Analysis

Multiple suspicious commands were observed.

### Payload Retrieval

```text
http://107.191.58.76/payload.exe
```

A malicious executable was downloaded from an external source.

---

### ASPX Web Shell Activity

Observed file:

```text
spinstall0.aspx
```

Location:

```text
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\16\TEMPLATE\LAYOUTS\
```

This location is associated with Microsoft SharePoint components and is frequently targeted during SharePoint exploitation.

---

### Dynamic Compilation

The following activity was identified:

```text
payload.cs
```

compiled through:

```text
csc.exe
```

which generated:

```text
payload.exe
```

This indicates that attacker-controlled code was compiled and executed directly on the SharePoint server.

---

### Encoded PowerShell Execution

Observed command:

```text
powershell.exe -nop -w hidden -e
```

Characteristics:

```text
-nop
-w hidden
-e
```

These parameters indicate:

- No PowerShell profile loading
- Hidden execution window
- Base64 encoded PowerShell commands

This behavior is commonly associated with malicious execution and defense evasion.

---

## Attack Chain Reconstruction

```text
Authentication Bypass
           ↓
Payload Delivery
           ↓
payload.exe Downloaded
           ↓
spinstall0.aspx Created
           ↓
payload.cs Generated
           ↓
csc.exe Compilation
           ↓
payload.exe Execution
           ↓
Encoded PowerShell Execution
```

---

## Indicators of Compromise (IOCs)

### External IP Address

```text
107.191.58.76
```

### Payload

```text
payload.exe
```

### Source Code File

```text
payload.cs
```

### ASPX File

```text
spinstall0.aspx
```

### PowerShell Execution

```text
powershell.exe -nop -w hidden -e
```

---

## Findings Summary

The investigation confirmed:

- A SharePoint server was targeted through a ToolShell-style exploitation attempt.
- Malicious code was downloaded from external infrastructure.
- An ASPX file was created within a SharePoint application directory.
- C# source code was compiled locally using csc.exe.
- Payload execution occurred on the server.
- Encoded PowerShell commands were executed.
- Activity was consistent with successful remote code execution.

---

## Verdict

### True Positive

The alert was confirmed as a legitimate SharePoint exploitation incident.

Evidence demonstrated payload delivery, compilation of malicious code, PowerShell abuse, and remote code execution activity on the affected SharePoint server.

---

## Response Actions

- Investigated endpoint telemetry.
- Reviewed terminal history.
- Identified malicious payloads.
- Documented attacker infrastructure.
- Confirmed PowerShell abuse.
- Confirmed code compilation and execution.
- Isolated the affected server.
- Documented identified IOCs.

---

## Lessons Learned

- SharePoint servers are high-value targets for authentication bypass and remote code execution attacks.
- ASPX files created in SharePoint directories should be treated as highly suspicious.
- Encoded PowerShell execution is a common post-exploitation technique.
- csc.exe abuse may indicate malicious code compilation directly on a server.
- Early containment is critical when exploitation of internet-facing services is detected.
