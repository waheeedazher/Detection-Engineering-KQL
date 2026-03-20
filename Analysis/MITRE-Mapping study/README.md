## MITRE ATT&CK Detection Mapping

This study documents common enterprise attack behaviors and maps them to observable telemetry and detection logic within Microsoft Sentinel.

The focus is on translating MITRE ATT&CK techniques into practical detection opportunities using available log sources such as Defender for Endpoint and Entra ID.

---

## Overview

The work is structured as a detection catalog, where each entry connects:

* Attacker behavior
* Observable system activity
* Relevant log source
* Detection logic and KQL
* MITRE ATT&CK technique and tactic

This mapping ensures that each detection is grounded in real telemetry rather than theoretical coverage.

---

## Scope

* Covers multiple stages of the attack lifecycle including:

  * Initial Access
  * Execution
  * Persistence
  * Privilege Escalation
  * Defense Evasion
  * Credential Access
  * Discovery
  * Lateral Movement
  * Command and Control
  * Exfiltration

* Focuses on behaviors that are:

  * Common in enterprise intrusions
  * Detectable using standard telemetry
  * Relevant to SOC monitoring workflows

---

## Key Takeaways

* Effective detection depends on **telemetry availability**, not just technique knowledge
* Certain behaviors (e.g., process execution, authentication) have strong visibility, while others rely on limited signals
* Parent-child process relationships and command-line context are critical for high-confidence detections
* Many high-impact techniques can be detected using relatively simple logic when mapped correctly

---

## Structure

Each behavior in the catalog includes:

* Technique and tactic mapping (MITRE ATT&CK)
* Example attacker activity
* Relevant Microsoft Sentinel log sources
* Detection logic explanation
* Example KQL query

---

## Notes

* Detection logic is designed for practical SOC use but may require tuning based on environment-specific baselines
* Some mappings are based on controlled observations and do not represent full production coverage
* The emphasis is on building detection reasoning rather than exhaustive coverage

---

## Reference

Full detailed catalog available in:

* `Mitre based attack behaviours.docx`
