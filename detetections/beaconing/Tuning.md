# Tuning & False Positive Analysis

## Overview

This document presents the tuning methodology, identified false positives, and exclusion logic applied to the Network Beaconing Detection rule.

The objective is to minimize false positives while maintaining high detection fidelity for true malicious activity.

---

## Tuning Methodology

The following structured approach was applied:

1. **Baseline Collection**

   * Collected 7–14 days of network telemetry
   * Identified recurring communication patterns across hosts

2. **Pattern Analysis**

   * Evaluated:

     * Connection frequency
     * Interval consistency (standard deviation)
     * Data transfer characteristics

3. **Classification**

   * Categorized activity into:

     * Legitimate periodic traffic
     * Suspicious or unknown behavior

4. **Controlled Exclusions**

   * Applied exclusions only after confirming:

     * Verified service ownership
     * Expected and documented behavior
     * Acceptable security risk

---

## Common False Positives

### 1. Microsoft Telemetry

**Example Destinations:**

* `v10.events.data.microsoft.com`

**Behavior:**

* Regular heartbeat communication
* Low jitter with consistent intervals

**Reason for False Positive:**

* Closely resembles beaconing patterns

**Tuning Strategy:**

```kql
| where RemoteIP !in (known_msft_ips)
```

**Risk Consideration:**

* Potential misuse of Microsoft infrastructure by attackers, though unlikely

---

### 2. Browser Background Activity

**Processes:**

* `chrome.exe`
* `msedge.exe`

**Behavior:**

* Periodic synchronization, push notifications, and extension activity

**Reason for False Positive:**

* Generates consistent outbound connections

**Tuning Strategy:**

```kql
| where InitiatingProcessFileName !in~ ("chrome.exe", "msedge.exe")
```

**Risk Consideration:**

* Malicious activity injected into browser processes may be overlooked

---

### 3. Antivirus / EDR Updates

**Processes:**

* Microsoft Defender and third-party security agents

**Behavior:**

* Scheduled updates and periodic communication with cloud services

**Tuning Strategy:**

* Allowlist verified update domains and IP ranges

**Risk Consideration:**

* Compromise of update channels, while rare, could have significant impact

---

### 4. Cloud / SaaS Services

**Examples:**

* Office 365 endpoints
* API-based services

**Behavior:**

* Regular polling and service communication with low jitter

**Tuning Strategy:**

* Establish organizational baselines
* Exclude high-confidence SaaS endpoints

**Risk Consideration:**

* Potential for attackers to leverage trusted cloud services for command and control

---

## Threshold Tuning

| Parameter        | Initial Value | Tuning Consideration                                   |
| ---------------- | ------------- | ------------------------------------------------------ |
| min_connections  | 20            | Increase to reduce noise in high-volume environments   |
| stdev_threshold  | 5             | Adjust based on observed variability in benign traffic |
| jitter_tolerance | 0.2           | Increase if environmental variability is higher        |

---

## Exclusion Principles

Exclusions are applied only when all of the following criteria are met:

* Traffic is verified as legitimate
* Behavior is consistent across multiple hosts or users
* No overlap with known attack techniques
* Approved through security review processes

---

## Monitoring Strategy

* Conduct monthly reviews of applied exclusions
* Revalidate against updated threat intelligence
* Monitor detection volume and effectiveness before and after tuning adjustments

---

## Known Gaps

* Low-frequency beaconing may evade detection
* CDN-based command-and-control traffic may blend with legitimate services
* Domain-based detection enhancements are not yet implemented

---
