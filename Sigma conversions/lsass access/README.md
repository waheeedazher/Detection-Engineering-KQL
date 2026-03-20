# LSASS Access Detection (Sigma to KQL)

## Objective
Detect suspicious access or interaction with the LSASS process, which may indicate credential dumping activity.

---

## Sigma Rule Summary
The original Sigma rule detects access to `lsass.exe` using the `process_access` category.

### Key Logic
- Target process: lsass.exe
- Condition: access to LSASS process

---

## Challenges in Translation

### 1. Log Source Gap
Sigma uses:
- `category: process_access`

In Microsoft Sentinel:
- Direct equivalent telemetry is not always available
- Approximated using `DeviceProcessEvents`

---

### 2. Field Mapping

| Sigma Field   | Sentinel Equivalent        |
|--------------|--------------------------|
| TargetImage  | FileName / ProcessCommandLine |

