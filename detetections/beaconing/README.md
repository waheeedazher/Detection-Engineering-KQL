# Network Beaconing & C2 Activity Detection

## Overview

This detection identifies potential Command-and-Control (C2) communication by analyzing the periodicity of outbound network traffic.

Rather than relying on static Indicators of Compromise (IoCs), this approach focuses on behavioral patterns. Many malware families maintain persistence by periodically "beaconing" to attacker-controlled infrastructure to receive instructions or maintain connectivity.

The detection leverages statistical analysis to identify automated, repetitive communication patterns that deviate from typical user-driven network activity.

---

## Detection Methodology

The detection follows a behavioral approach implemented in four stages:

### 1. Traffic Filtering

* Focuses on successful outbound network connections
* Excludes private/internal IP ranges to remove East-West traffic noise
* Operates on endpoint network telemetry (e.g., DeviceNetworkEvents)

> Note: While web ports are commonly used for C2, this detection is not inherently restricted to specific ports and can be extended to broader traffic.

---

### 2. Session Contextualization

Traffic is grouped into unique communication tuples to maintain high-fidelity tracking:

* DeviceName
* RemoteIP
* RemotePort
* InitiatingProcessFileName

This ensures that periodic behavior is evaluated per communication channel rather than across mixed traffic.

---

### 3. Statistical Analysis (Beaconing Behavior)

The detection models the "heartbeat" behavior of beaconing using time-based analysis:

* **Time Delta Calculation**
  Computes the time difference between consecutive connections using `prev()`

* **Average Interval (`avg_delta`)**
  Represents the typical beacon interval

* **Standard Deviation (`stdev_delta`)**
  Measures consistency of the intervals
  Low deviation indicates automated, periodic behavior

* **Jitter Ratio**
  Calculates relative variance (`stdev / avg`) to detect beaconing even when slight randomness is introduced

---

### 4. Behavioral Thresholding

An alert is generated when the following conditions are met:

* **Sufficient Activity**
  Minimum number of connections to ensure statistical reliability

* **Low Variance**
  Consistent time intervals between connections

* **Low Jitter Ratio**
  Indicates controlled periodic behavior even with minor randomization

---

## Detection Assumptions

This detection operates under the following assumptions:

* Beaconing communication maintains some level of periodicity, even with jitter
* Enough connection events exist to establish statistical significance
* Network telemetry provides accurate timestamps and process context

If these assumptions are not met, detection effectiveness may be reduced.

