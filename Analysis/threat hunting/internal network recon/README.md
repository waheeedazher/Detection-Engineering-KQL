## Threat Hunt: Internal Network Reconnaissance

This hunt investigates potential internal network reconnaissance activity within the environment, focusing on behaviors such as host discovery, port scanning, and abnormal connection patterns.

---

## Objective

To identify signs of internal reconnaissance that may indicate an attacker preparing for lateral movement.

---

## Hypothesis

If a host is compromised, it may perform network discovery by:

* Connecting to a large number of unique IP addresses
* Communicating across multiple destination ports
* Generating high volumes of connections within short time windows

---

## Approach

The hunt was conducted using a progressive analysis model:

* Identification of hosts with unusually high numbers of unique connections
* Analysis of port diversity to detect scanning behavior
* Baseline comparison of connection volume across endpoints
* Attribution of network activity to originating processes
* Validation of destination patterns and service usage

Primary data source:

* `DeviceNetworkEvents`

---

## Key Findings

* High connection volumes were observed but aligned with normal endpoint behavior
* Activity was primarily driven by browsers, system processes, and cloud services
* No abnormal port scanning or internal reconnaissance patterns were identified

---

## Outcome

* No evidence of malicious internal reconnaissance was found
* Established a baseline for normal network behavior within the environment
* Identified patterns useful for future detection logic

---

## Detection Opportunities

* Monitor for rapid bursts of connections within short time windows
* Detect hosts communicating with unusually high numbers of internal IPs
* Track abnormal port distribution patterns across endpoints

---

## Notes

* Sensitive telemetry and raw outputs have been omitted
* Findings are based on available data and scoped time window
* Detection thresholds require tuning based on environment-specific baselines

---

## Reference

Full hunt report available in:

* `Threat Hunting Report.pdf`
