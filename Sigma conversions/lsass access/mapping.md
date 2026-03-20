# Field Mapping – LSASS Access Detection

## Log Source Mapping

| Sigma Logsource        | Sentinel Equivalent        | Notes |
|----------------------|--------------------------|------|
| product: windows     | Microsoft Defender XDR   | Based on available telemetry |
| category: process_access | No direct equivalent | Approximated using process telemetry |

---

## Table Selection

Selected:
- DeviceProcessEvents

### Justification:
Sigma specifies `process_access`, which typically refers to process handle access events.

Microsoft Sentinel does not natively expose direct process access events in standard tables.

DeviceProcessEvents was selected as the closest approximation to:
- Identify process interactions
- Analyze command-line behavior

---

## Field Mapping

| Sigma Field   | Sentinel Field              | Reason |
|--------------|---------------------------|--------|
| TargetImage  | FileName                  | Represents target process name |
| TargetImage  | ProcessCommandLine        | Provides additional context for interaction |

---

## Modifier Mapping

| Sigma Modifier | KQL Equivalent |
|--------------|----------------|
| endswith     | endswith       |

---

## Detection Logic Interpretation

Original Sigma Logic:
- Detect access to `lsass.exe`

Interpretation in Sentinel:
- Direct process access telemetry unavailable
- Detection adapted to identify processes referencing LSASS

---

## Limitations

- No direct mapping for process handle access
- Detection relies on indirect indicators
- May miss low-level credential dumping techniques

---

## Key Insight

Mapping is not 1:1 translation.

It requires:
- Understanding of telemetry gaps
- Context-driven approximation
- Detection intent preservation
