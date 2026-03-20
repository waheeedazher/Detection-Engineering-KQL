## SOC Metrics Accuracy Study

This analysis examines how SOC efficiency metrics in Microsoft Sentinel workbooks are derived and why they can be misleading if interpreted without context.

The focus is on identifying gaps between what the dashboard presents and what is actually happening in SOC operations.

---

## Overview

The study reviews key workbook metrics including:

* Incident volume trends
* Classification metrics
* Severity distribution
* Ownership and workload metrics
* Response and closure times (MTTT / MTTR)

It highlights how filtering logic, incident lifecycle behavior, and operational constraints influence these metrics.

---

## Key Observations

* Incident volume does not directly represent threat activity due to alert grouping and merging
* MTTR and MTTT reflect elapsed time, not actual analyst responsiveness
* Ownership metrics attribute work to the final owner, ignoring investigation history
* Severity trends are heavily influenced by detection logic and correlation, not just attacker activity
* High "Undetermined" classifications often indicate effective deduplication rather than poor investigation

---

## Core Insight

Workbook metrics represent a **filtered and aggregated view of SOC activity**, not an absolute measure of:

* Analyst performance
* Threat volume
* Detection quality

Accurate interpretation requires understanding:

* Incident lifecycle behavior
* Merging and correlation logic
* Scope and filter constraints

---

## Outcome

* Identified key sources of metric distortion in SOC dashboards
* Highlighted common misinterpretations at both analyst and management levels
* Established a framework to differentiate between analyst, process, and system-driven delays
* Establishes a baseline for identifying gaps in workbook logic and metric interpretation  
* Forms the foundation for further analysis and refinement of workbook calculations to improve accuracy and reliability of reported metrics  ---

## Notes

* This analysis is based on observed workbook behavior and available data structures
* Some operational scenarios have been generalized to remove sensitive details
* The focus is on interpretation accuracy rather than workbook configuration

---

## Reference

Full document available in:

* `SOC efficiency workbook review.docx`
