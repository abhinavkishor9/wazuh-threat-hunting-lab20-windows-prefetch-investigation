# wazuh-threat-hunting-lab20-windows-prefetch-investigation
## Overview

Windows Prefetch is a forensic artifact that records information about executed applications to improve application startup performance. During digital forensic investigations, Prefetch files help analysts determine whether an executable was run, even if the original executable has been deleted.

This lab demonstrates how to investigate Windows Prefetch artifacts and correlate them with Sysmon Event ID 1 (Process Creation) and Wazuh Threat Hunting.

---

# Lab Objectives

- Understand the purpose of Windows Prefetch
- Execute common Windows applications
- Verify Prefetch file creation
- Investigate Sysmon Process Creation events
- Correlate execution evidence using Wazuh
- Build a forensic execution timeline

---

# Lab Environment

## Endpoint

- Windows 11

## Monitoring

- Wazuh Agent
- Wazuh Manager
- Sysmon

## Tools

- PowerShell
- Windows Explorer
- Wazuh Dashboard

---

# Why Prefetch Matters

Windows creates Prefetch files to improve application startup performance. These artifacts are also valuable during DFIR investigations because they provide evidence that an application was executed.

Prefetch can help investigators determine:

- Whether an application executed
- Recent execution activity
- Approximate execution count
- Last execution time
- Additional execution artifacts (using specialized forensic tools)

---

# Applications Executed

- Notepad
- Calculator
- Microsoft Paint
- Command Prompt

---

# Investigation Workflow

```
Application Execution
        ↓
Windows Prefetch (.pf)
        ↓
Sysmon Event ID 1
        ↓
Wazuh Agent
        ↓
Wazuh Manager
        ↓
Threat Hunting Investigation
```

---

# Investigation Steps

1. Verify Sysmon and Wazuh services.
2. Confirm Prefetch is enabled.
3. Execute multiple Windows applications.
4. Verify new Prefetch artifacts.
5. Investigate Sysmon Event ID 1.
6. Hunt process creation events in Wazuh.
7. Correlate Prefetch with Sysmon telemetry.
8. Build the execution timeline.

---

# Wazuh Queries

## Process Creation

```
data.win.system.eventID:1
```

## Process Name

```
notepad.exe
```

```
calc.exe
```

```
mspaint.exe
```

```
cmd.exe
```

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Execution | User Execution | T1204 |
| Execution | Command and Scripting Interpreter | T1059 |

---

# Investigation Summary

Multiple Windows applications were executed during the lab. Windows generated Prefetch artifacts for the executed applications, while Sysmon recorded corresponding Process Creation events (Event ID 1). Wazuh successfully collected and displayed the execution telemetry, allowing the complete execution timeline to be reconstructed.

---

# Skills Demonstrated

- Windows DFIR
- Windows Prefetch Analysis
- Process Execution Investigation
- Sysmon Analysis
- Wazuh Threat Hunting
- Timeline Reconstruction
- Windows Forensics
- SOC Investigation

---

# Learning Outcome

This lab demonstrates how Windows Prefetch artifacts complement endpoint telemetry by providing additional forensic evidence of application execution. Combining Prefetch artifacts with Sysmon and Wazuh improves confidence during incident investigations and malware analysis.
