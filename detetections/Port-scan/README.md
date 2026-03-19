# Network Port Scan Detection

## Overview

This detection identifies potential port scanning activity by monitoring outbound connection attempts from a single host to multiple destination ports or IP addresses within a defined time window.

Port scanning is commonly used during the reconnaissance phase of an attack to identify open services, misconfigurations, or vulnerable systems. Detecting this behavior early enables proactive response before exploitation or lateral movement occurs.

This detection focuses on identifying abnormal connection patterns that deviate from typical user or application behavior.

---

## Detection Methodology

The detection follows a behavioral approach based on connection distribution:

### 1. Traffic Filtering

* Focuses on outbound network connections
* Excludes private/internal IP ranges to reduce internal noise
* Uses endpoint telemetry (e.g., DeviceNetworkEvents)

---

### 2. Behavioral Indicators

Port scanning behavior is characterized by:

* A single source communicating with multiple destination ports (vertical scan), or
* A single source communicating with multiple destination IPs (horizontal scan)

---

### 3. Aggregation Logic

The detection aggregates network activity over a short time window and evaluates:

* Number of unique destination ports
* Number of unique destination IPs
* Total connection attempts

---

### 4. Threshold-Based Detection

An alert is generated when:

* A host connects to a high number of unique ports or IPs
* Activity occurs within a short time window
* The pattern deviates from expected application behavior

---

## Detection Assumptions

* Port scanning generates a high volume of connection attempts within a limited timeframe
* Normal user or application traffic does not typically access many ports or hosts rapidly
* Network telemetry accurately reflects connection attempts


---

## Validation Summary

This detection was tested in a controlled lab environment using simulated scanning tools.

**Observed Results:**

* Successfully detected rapid port scanning behavior (e.g., Nmap scans)
* Identified both:

  * Vertical scans (single IP, multiple ports)
  * Horizontal scans (multiple IPs, same port)

---

## Investigation Guidance

When triggered:

1. **Process Analysis**

   * Identify the initiating process
   * Common suspicious tools:

     * `nmap.exe`
     * `powershell.exe`
     * unknown binaries

2. **Scan Pattern**

   * Determine if the scan is:

     * Vertical (ports)
     * Horizontal (IPs)

3. **Target Analysis**

   * Are targets internal, external, or sensitive assets?

4. **User Context**

   * Is the activity expected (e.g., security team, scanner account)?

5. **Packet size**

   * What was the packet size, was the packet empty (e.g., SYN packet, ACK packet)?

---

## Detection Limitations

* Slow or stealth scans may evade detection
* Legitimate scanning tools may generate false positives
* Does not distinguish between benign and malicious intent without context

