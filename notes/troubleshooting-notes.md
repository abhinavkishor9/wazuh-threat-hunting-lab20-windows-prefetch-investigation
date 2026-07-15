# Troubleshooting Notes

## Issue 1

### Prefetch folder is empty

Cause

Windows Prefetch may be disabled or the system has not generated recent Prefetch artifacts.

Resolution

Verify that the Prefetch directory exists:

```
C:\Windows\Prefetch
```

Run several applications and check the directory again.

---

## Issue 2

### No new Prefetch files created

Cause

The application may have already been executed recently or the Prefetch file already exists.

Resolution

Sort the Prefetch directory by **Last Modified** to identify recently updated files:

```powershell
Get-ChildItem C:\Windows\Prefetch |
Sort-Object LastWriteTime -Descending
```

---

## Issue 3

### No Sysmon Event ID 1

Cause

Sysmon Process Creation monitoring is disabled or events have not yet been generated.

Resolution

Verify Sysmon is running:

```powershell
Get-Service Sysmon64
```

Execute an application again and check the Sysmon Operational log.

---

## Issue 4

### No results in Wazuh

Cause

Events have not yet been indexed or the dashboard time range is incorrect.

Resolution

- Set the Wazuh time range to **Last 15 Minutes** or **Last 1 Hour**.
- Refresh the Threat Hunting page.
- Search:

```
data.win.system.eventID:1
```

---

## Issue 5

### Unable to locate the executed application

Cause

The application may have generated multiple Process Creation events.

Resolution

Search directly by process name:

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

## Issue 6

### Prefetch timestamps do not match execution time exactly

Cause

Windows updates Prefetch metadata as part of its performance optimization process, so timestamps may differ slightly from the exact execution time.

Resolution

Correlate Prefetch timestamps with Sysmon Event ID 1 and Wazuh logs rather than relying on Prefetch alone.

---

# Lessons Learned

- Prefetch artifacts provide valuable evidence that an application was executed.
- Sysmon Event ID 1 supplies detailed process execution information.
- Wazuh centralizes endpoint telemetry for efficient investigation.
- Correlating multiple forensic artifacts produces stronger and more reliable investigation results than relying on a single source.

---

# Final Status

✅ Sysmon verified

✅ Wazuh Agent verified

✅ Prefetch artifacts identified

✅ Process Creation events collected

✅ Wazuh investigation completed

✅ Execution timeline reconstructed

The lab successfully demonstrated how Windows Prefetch artifacts enhance DFIR investigations by providing additional evidence of application execution alongside Sysmon and Wazuh telemetry.
