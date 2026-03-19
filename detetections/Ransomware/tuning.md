# Tuning & False Positive Analysis

## Overview

This document outlines tuning strategies and presumed false positive analysis for the Early-Stage Ransomware Detection rule.

The goal is to balance early detection with manageable alert volume.

---

## Tuning Methodology

1. **Baseline Analysis**

   * Reviewed file activity patterns across endpoints
   * Identified processes generating high file modification rates

2. **Behavioral Correlation**

   * Prioritized signals that rarely occur together in normal environments

3. **Score Calibration**

   * Adjusted weights to ensure:

     * High-risk behaviors generate high confidence
     * Single benign signals do not trigger alerts

---

## Common False Positives

### 1. Software Updates / Installers

**Behavior:**

* High volume of file modifications

**Examples:**

* OS updates
* Application installations

**Tuning Strategy:**

//add filter to ignore specific administrative processes
| where InitiatingProcessFileName !in ("trusted_installer.exe")


**Risk Consideration:**

* Malicious processes masquerading as installers or if trusted proccess are abused then the detection will collapse

---

### 2. Backup Solutions

**Behavior:**

* Large-scale file access/modification

**Tuning Strategy:**

* Allowlist known backup processes

---

### 3. Administrative Scripts

**Behavior:**

* Use of PowerShell or command-line tools

**Tuning Strategy:**

* Baseline known administrative activity
* Exclude approved scripts

---

### 4. Security Tools

**Behavior:**

* May trigger shadow copy operations or file access

**Tuning Strategy:**

* Identify and allowlist trusted security tools

---

## Threshold Tuning

| Parameter      | Initial Value | Tuning Consideration                        |
| -------------- | ------------- | ------------------------------------------- |
| file_threshold | 100           | Adjust based on normal file activity levels |
| score weights  | 2 / 4         | Increase weight for high-confidence signals |

---

## Exclusion Principles

* Only exclude verified legitimate processes
* Avoid broad exclusions (e.g., excluding PowerShell entirely)
* Maintain visibility into high-risk behaviors

---

## Monitoring Strategy

* Continuously review alerts for accuracy
* Adjust thresholds based on environment behavior
* Validate detection against real incidents

---

## Known Gaps

* File-less ransomware may evade detection
* Slow encryption may bypass thresholds
* Requires correlation with additional signals for full coverage

---

## Key Consideration
Tuning should be done continuously and theoritically this detection rule demands high number of resources to deploy and maintain
