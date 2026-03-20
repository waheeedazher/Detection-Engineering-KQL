
## Detection Posture Assessment

This analysis evaluates detection capability across email, endpoint, and identity domains from a SOC visibility and control perspective.

The focus is on determining whether detection capabilities are supported by available telemetry and actionable detection logic at the SIEM level.

---

## Overview

The assessment examines:

* Whether relevant telemetry is available
* Whether analytics exist to convert telemetry into detections
* Whether detections are visible and actionable at the SOC layer

Detection capability is categorized as:

* **Detected** – telemetry and analytics present
* **Visible but Undetected** – telemetry present but no detection logic
* **Blind Spot** – required telemetry absent

---

## Key Findings

* Email-based initial access lacks SIEM-side detection despite available telemetry
* Endpoint detection relies heavily on upstream verdicts, limiting behavioral visibility
* Identity detections exist but lack explainability in certain scenarios

These gaps impact the SOC’s ability to independently detect and investigate early-stage attacker activity.

---

## Gap Summary

* **Email Detection Gap**

  * No independent detection for malicious email delivery
  * Reliance on upstream controls and user reporting

* **Endpoint Visibility Gap**

  * Limited visibility into pre-verdict behavior
  * Reduced context for investigation

* **Identity Explainability Gap**

  * Detection present but lacks clarity for consistent triage

---

## Outcome

* Identified gaps in detection coverage and control ownership
* Highlighted areas where telemetry exists but is not operationalized
* Provided recommendations to improve SOC-level visibility and detection capability

---

## Notes

* This assessment focuses on detection visibility, not incident response or tool effectiveness
* Findings are based on available telemetry and observed detection logic
* Some details have been generalized to remove sensitive information

---

## Reference

Full report available in:

* `Soc Detection Posture Assessment Report.pdf`
