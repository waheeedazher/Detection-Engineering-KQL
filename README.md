# Detection Engineering Portfolio — Microsoft Sentinel & KQL

## Overview

This repository showcases practical **Detection Engineering** capabilities using Microsoft Sentinel, KQL, and threat-informed methodologies. It demonstrates the end-to-end lifecycle of detection development — from attack simulation and telemetry generation to detection tuning, validation, and coverage analysis.

The focus is on building **high-fidelity detections**, reducing false positives, and improving SOC efficiency through structured engineering practices.

---

## Key Capabilities Demonstrated

* Detection development using **Kusto Query Language (KQL)**
* Threat-informed detection aligned with **MITRE ATT&CK**
* Detection tuning and **false positive reduction**
* **Attack simulation & validation** in lab environments
* Detection coverage analysis & **gap identification**
* Cross-platform detection using **Sigma rules**
* SOC optimization through **metrics and prioritization logic**

---

## Repository Structure

### Detection Engineering Lab

Simulated real-world attack scenarios to design and validate detections.

**Includes:**

* Credential dumping detection
* PowerShell abuse detection
* Beaconing activity detection
* Network scanning detection

**Focus:**

* Detection logic development
* Telemetry analysis
* Pre-production validation

---

### Detection Coverage & Gap Analysis

Structured evaluation of detection posture using MITRE ATT&CK.

**Includes:**

* MITRE ATT&CK mapping
* Coverage heatmap
* Identification of detection gaps

**Outcome:**

* Improved visibility into monitored vs unmonitored attack techniques
* Prioritized areas for detection enhancement

---

### Detection Optimization & SOC Efficiency

Focused on improving alert quality and reducing analyst workload.

**Includes:**

* False positive analysis and reduction
* Detection threshold tuning
* Alert prioritization logic

**Impact:**

* Improved signal-to-noise ratio
* Reduced manual triage effort

---

### Sigma Rule Conversion

Conversion of KQL detections into Sigma rules for platform-agnostic use.

**Purpose:**

* Enable reuse across different SIEM platforms
* Standardize detection logic

---

## Detection Engineering Approach

The work in this repository follows a structured detection engineering lifecycle:

1. **Simulate Attack Behavior**
   Recreate adversary techniques in a controlled lab environment

2. **Analyze Telemetry**
   Identify relevant logs across endpoint, identity, and network sources

3. **Develop Detection Logic**
   Write KQL queries aligned with attack patterns

4. **Validate & Tune**
   Reduce false positives and improve detection fidelity

5. **Map to MITRE ATT&CK**
   Ensure coverage across known adversary techniques

6. **Measure & Improve**
   Continuously refine detections using metrics and testing

---

## Tools & Technologies

* Microsoft Sentinel
* Microsoft Defender XDR
* Kusto Query Language (KQL)
* Sigma
* MITRE ATT&CK Framework

---

## Sample Outcomes

* Developed detections across **endpoint, identity, and network telemetry**
* Reduced false positives through **threshold tuning and filtering**
* Built structured detection coverage across **20+ MITRE ATT&CK techniques**
* Identified critical gaps in detection visibility and proposed improvements
* Created reusable detection logic for cross-platform environments

---

## About Me

Detection Engineer with hands-on experience in Microsoft Sentinel environments, focused on building reliable, high-quality detections and improving SOC effectiveness.

* Experience in real-world alert triage and incident handling
* Strong focus on detection accuracy and engineering mindset
* Actively working toward Microsoft SC-200 certification

---

## Contact

* LinkedIn: [https://www.linkedin.com/in/waheedazher/]
* Email: [waheedazher14@gmail.com](mailto:waheedazher14@gmail.com)

---

## Notes

This repository is continuously updated with new detections, improvements, and validation techniques, reflecting ongoing learning and hands-on experimentation.
