# Tuning & False Positive Analysis

## Overview

This document outlines the tuning strategy and false positive analysis for the Port Scan Detection rule.

The objective is to reduce alert noise while maintaining visibility into reconnaissance activity.

---

## Tuning Methodology

1. **Baseline Analysis**

   * Reviewed 7–14 days of network activity
   * Identified hosts with high connection diversity

2. **Behavior Classification**

   * Distinguished between:

     * Normal application behavior
     * Administrative/scanning tools
     * Suspicious activity

3. **Threshold Calibration**

   * Adjusted thresholds to balance:

     * Detection sensitivity
     * False positive reduction

---

## Common False Positives

### 1. Vulnerability Scanners

**Examples:**

* Nessus
* Qualys
* OpenVAS

**Behavior:**

* High number of ports scanned across multiple hosts

**Tuning Strategy:**

```kql
| where DeviceName !in (scanner_hosts)
```

**Risk Consideration:**

* Compromised scanner systems could be missed

---

### 2. IT Monitoring Tools

**Examples:**

* Network monitoring agents
* Health check scripts

**Behavior:**

* Regular checks across multiple ports/services

**Tuning Strategy:**

* Baseline known monitoring systems
* Exclude verified service accounts or hosts

---

### 3. Software Deployment Systems

**Behavior:**

* Connections to multiple endpoints during deployment

**Tuning Strategy:**

* Identify deployment windows
* Correlate with change management records

---

### 4. Security Testing Activities

**Behavior:**

* Internal red team or pentesting scans

**Tuning Strategy:**

* Maintain allowlist for approved testing assets

---

## Threshold Tuning

| Parameter            | Initial Value | Tuning Consideration                           |
| -------------------- | ------------- | ---------------------------------------------- |
| port_threshold       | 20            | Increase if environment has many service calls |
| ip_threshold         | 15            | Adjust based on network size                   |
| connection_threshold | 50            | Helps filter low-volume noise                  |

---

## Exclusion Principles

Exclusions are applied only when:

* Activity is verified as legitimate
* Source system is known and documented
* Behavior is consistent and expected
* Risk of exclusion is accepted

---

## Monitoring Strategy

* Review detection alerts weekly
* Revalidate exclusions periodically
* Adjust thresholds based on environment changes

---

## Known Gaps

* Slow or distributed scans may evade detection
* Encrypted traffic limits visibility into intent
* High-noise environments may require aggressive tuning

---
