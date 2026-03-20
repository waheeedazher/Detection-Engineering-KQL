# Sigma Rule to KQL Conversion Lab

## Overview
This repository demonstrates the translation of Sigma detection rules into Microsoft Sentinel (KQL) queries.

The focus is not just conversion, but understanding how platform-agnostic detection logic maps to real-world telemetry and constraints within a SIEM environment.

---

## Objectives
- Translate Sigma rules into KQL
- Map generic fields to Sentinel-specific schemas
- Identify gaps and limitations in translation
- Demonstrate detection engineering thought process

---

## Methodology

### 1. Rule Analysis
Each Sigma rule is reviewed to understand:
- Detection intent
- Log source category
- Key indicators

### 2. Field Mapping
Sigma fields are mapped to Microsoft Sentinel tables such as:
- DeviceProcessEvents
- DeviceNetworkEvents
- SecurityEvent

### 3. Query Translation
Rules are converted using Sigma CLI (Kusto backend) and then manually refined to:
- Align with available telemetry
- Improve detection accuracy
- Reduce false positives

### 4. Validation Considerations
- Identified potential false positives
- Highlighted assumptions due to missing telemetry
- Included tuning recommendations

---

## Key Challenges

- Sigma rules are platform-agnostic; Sentinel is schema-dependent
- Field mismatches (e.g., TargetImage vs FileName)
- Some Sigma logic cannot be directly translated
- Requires interpretation, not direct conversion

---

## Repository Structure

Each rule contains:

- `sigma.yml` → Original Sigma rule
- `kql.txt` → Final KQL query (manually refined)
- `mapping.md` → Field mapping and translation logic
- `notes.md` → Assumptions, limitations, and tuning insights

---

## Tools Used
- Sigma CLI (pySigma)
- Kusto (KQL)
- Microsoft Sentinel schema references

---

## Disclaimer
Some conversions are theoretical and not validated in a production environment due to limited telemetry access. The focus is on demonstrating detection engineering methodology.
