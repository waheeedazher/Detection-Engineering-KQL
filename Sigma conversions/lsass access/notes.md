# Detection Refinement Notes – LSASS Access

## Initial State
The Sigma conversion produced a minimal query:

TargetImage endswith "\\lsass.exe"

This output lacked:
- Table context
- Field mapping
- Detection clarity

---

## Issues Identified

1. No Data Source Mapping
- Sigma is platform-agnostic
- No direct reference to Sentinel tables

2. Incorrect Detection Focus
- Detects LSASS execution (normal behavior)
- Does not detect suspicious access

3. High False Positive Risk
- LSASS runs on all Windows systems
- Would generate constant noise

---

## Refinement Approach

### Step 1: Identify Equivalent Telemetry
- Used DeviceProcessEvents as closest approximation
- Acknowledged limitation (no direct process_access equivalent)

---

### Step 2: Field Mapping
- TargetImage → FileName / ProcessCommandLine

---

### Step 3: Improve Detection Logic
- Shifted focus from LSASS execution to interaction patterns
- Introduced filtering for known legitimate processes

---

### Step 4: False Positive Reduction
- Excluded:
  - lsass.exe
  - wininit.exe

---

## Key Insight

Sigma conversion provides syntactic translation, not operational detection logic.

Effective detection engineering requires:
- Understanding telemetry
- Contextual adaptation
- Iterative refinement

---

## Future Improvements

- Incorporate Sysmon Event ID 10 (ProcessAccess)
- Add parent-child process relationships
- Use anomaly-based detection for rare access patterns
