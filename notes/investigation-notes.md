# Investigation Notes

## Incident Summary

A forensic investigation was conducted to determine whether multiple Windows applications had been executed on the monitored endpoint.

Windows Prefetch artifacts were correlated with Sysmon Process Creation events and Wazuh telemetry to validate execution.

---

# Timeline

## Step 1

Verified monitoring services.

Observed

- Sysmon Service Running
- Wazuh Agent Running

---

## Step 2

Verified Windows Prefetch directory.

Observed

Existing Prefetch (.pf) files were present, confirming Prefetch was enabled.

---

## Step 3

Executed Windows applications.

Applications

- notepad.exe
- calc.exe
- mspaint.exe
- cmd.exe

---

## Step 4

Verified Prefetch artifacts.

Observed

Recent Prefetch files corresponding to the executed applications.

Examples

- NOTEPAD.EXE-XXXXXXXX.pf
- CALC.EXE-XXXXXXXX.pf
- MSPAINT.EXE-XXXXXXXX.pf
- CMD.EXE-XXXXXXXX.pf

---

## Step 5

Investigated Sysmon Event ID 1.

Observed

Process Creation events for each executed application.

Verified

- Process Image
- Command Line
- User
- Timestamp

---

## Step 6

Investigated Wazuh telemetry.

Threat Hunting Query

```
data.win.system.eventID:1
```

Observed

Process execution events successfully ingested into Wazuh.

---

# Evidence Correlation

Application Executed

↓

Prefetch File Created

↓

Sysmon Event ID 1 Generated

↓

Wazuh Collected Telemetry

↓

SOC Investigation

---

# DFIR Analysis

Prefetch artifacts confirmed that the applications had been executed on the endpoint.

Sysmon Event ID 1 provided precise execution details including process image, command line, user account, and execution time.

The combination of Prefetch and Sysmon strengthened confidence in the investigation findings.

---

# MITRE ATT&CK

Execution

- T1204 – User Execution

Execution

- T1059 – Command and Scripting Interpreter (Command Prompt)

---

# Conclusion

The investigation successfully demonstrated how Windows Prefetch artifacts, Sysmon telemetry, and Wazuh Threat Hunting can be combined to validate application execution and reconstruct an accurate execution timeline during DFIR investigations.
