Network Beaconing & C2 Activity Detection

Overview

This detection module identifies potential Command-and-Control (C2) communication by analyzing the periodicity of outbound network traffic.
Modern malware maintains persistence by "beaconing"—sending rhythmic check-ins to an attacker-controlled listener to receive instructions or heartbeat signals. This detection bypasses static Indicator of Compromise (IoC) matching by using statistical analysis to find automated, repetitive connection patterns that deviate from human-generated web traffic.

Detection Methodology

The logic shifts away from static signatures toward a behavioral approach, executed in four distinct phases:
1. Traffic Normalization & Filtering

Directionality: Isolates successful outbound network connections.

Scope: Filters out internal East-West traffic by excluding RFC1918 private IP ranges.

Protocol Focus: Targets common C2 egress ports (e.g., 80, 443, 8080).

2. Session Contextualization

Traffic is aggregated into unique communication tuples to ensure high-fidelity tracking:

DeviceName + RemoteIP + RemotePort + InitiatingProcess

3. Statistical Analysis (The "Heartbeat" Logic)

The query employs Kusto’s serialization functions to calculate the "rhythm" of the connection:

Time Delta Calculation: Uses prev() to measure the exact time elapsed between consecutive outbound pulses.

Standard Deviation ($\sigma$): Measures the consistency of the intervals. A low $\sigma$ indicates a highly predictable, automated heartbeat.

Jitter Analysis: Calculates the ratio of variance to the average interval to identify "jittered" beacons designed to evade simple threshold alerts.

4. Behavioral Thresholds

An alert is generated only when a connection meets specific statistical criteria:

Persistence: Minimum threshold of unique connections (e.g., >30 pulses).

Consistency: A Standard Deviation near zero (high-confidence automation).


Visualization of the beaconing "pulse" in a lab environment.



