# Incident Response Playbook: Unauthorized Cryptomining

## Purpose
This playbook guides cybersecurity teams through responding to incidents involving unauthorized cryptocurrency mining (“cryptojacking”), defined as the deployment or use of mining software on corporate assets without authorization. The goal is to **detect**, **contain**, **eradicate**, and **recover** from such incidents while preserving evidence, minimizing business disruption, and improving defenses.

---

## Roles & Responsibilities

| Role | Responsibilities |
|---|---|
| **Incident Response Lead** | Oversees the response, ensures coordination, reports to management. |
| **Threat Hunt / SOC Analyst** | Runs the hunts, analyzes data, validates alerts, identifies affected systems. |
| **Forensic Analyst** | Preserves logs and artifacts, investigates timeline, identifies root cause. |
| **IT / System Admin** | Takes remediation actions—isolating hosts, disabling tasks, patching, cleaning up. |
| **Network / Security Engineering** | Blocks network paths, enforces firewall/IDS rules, updates watchlists/firewall rules. |
| **Legal / Compliance** | Determines notification obligations, preserves evidence chain. |
| **Communications** | Internal stakeholder updates, user messaging as needed. |

---

## Triage & Validation

1. **Alert / Detection Triggered**  
   - KQL query results from any of the lab’s detection queries (file, process, network, performance, scheduled task, composite).  
   - Potential triggers: high CPU/GPU usage off-hours, scheduled tasks with miner binary, outbound connections to mining pools, suspicious file artifacts.

2. **Gather Initial Data**  
   - Device name(s), user accounts involved.  
   - Time window of suspicious activity.  
   - Processes names (e.g. `xmrig.exe`, `miner.exe`, `ccminer.exe`, etc.).  
   - Filenames, paths, scheduled tasks.  
   - Remote IPs, ports, domains used (pool endpoints).  
   - Performance metrics (CPU / GPU utilization), especially during off-hours.

3. **Verify False Positives**  
   - Check whether tools are legitimate software (e.g., developer tools / GPU benchmarking / authorized test software).  
   - Confirm that the process is not already whitelisted.  
   - Check whether network endpoints correspond to known corporate assets or allowed domains.  
   - Confirm configuration (e.g., is this lab / test environment or production).

---

## Containment

1. **Isolate Affected Devices**  
   - If mining is active and unauthorized, isolate the device from the network to prevent further damage or spread.

2. **Stop Running Processes**  
   - Terminate miner processes (e.g., `xmrig.exe`, etc.).  
   - Kill any scheduled tasks configured for persistence.  
   - Block execution (apply application whitelisting or block via EDR/AV).

3. **Disconnect Network Paths**  
   - Block outbound traffic to known mining pool endpoints (domains, IPs, ports).  
   - Add stratum protocol ports (3333, 4444, 5555, etc.) to network firewall / perimeter blocking.

---

## Eradication

1. **Remove Files & Configurations**  
   - Delete miner binaries, configuration files (e.g. `*.exe`, `config.json`) from user directories and appdata.  
   - Remove or disable scheduled tasks and other persistence mechanisms.

2. **Patch & Harden**  
   - Ensure endpoint security (AV/EDR definitions) are up to date.  
   - Enforce least privilege so users shouldn't have admin rights that allow persistence installation.  
   - Implement software restriction policies (AppLocker / WDAC).  
   - Ensure logging / telemetry is enabled (file, process, scheduled tasks, network).

3. **Review Policies / Controls**  
   - Update or enforce policies around use of mining software (usually disallowed).  
   - Ensure internal training to raise awareness of cryptojacking risks.

---

## Recovery

1. **Restore Devices**  
   - Confirm devices are clean, performance has returned to baseline.  
   - Verify that process / file / network anomalies are resolved.  
   - Re-enable network connectivity once safe.

2. **Monitor Closely**  
   - Increase monitoring on affected devices for some time (e.g., 7–14 days) to detect any re-emergence.  
   - Run the lab’s KQL queries in scheduled hunts to detect re-deployments.

3. **Testing & Verification**  
   - Perform penetration tests or red-team exercises to attempt to reintroduce miner and ensure controls hold.  
   - Validate that blocked endpoints are indeed being blocked.

---

## Post-Incident Learning & Improvements

| Area | Possible Improvement |
|---|------------------------|
| **Detection** | Add more watchlists for mining pool domains / IPs; build detection for uncommon ports; improve composite correlation queries. |
| **Prevention** | Harden endpoints; enforce policy; restrict privilege to install software; whitelist allowed applications. |
| **Response Process** | Streamline containment & eradication workflows; ensure forensic readiness; update IR runbooks. |
| **Awareness & Training** | Train users to report unusual performance; raise awareness of cryptojacking techniques. |
| **Automation** | Automate alerting when performance thresholds are reached or unexpected outbound connections to mining pool endpoints are detected. |

---

## Evidence & Forensics

- Collect and preserve logs from:
  1. **File events** (when miner binaries were created or modified).  
  2. **Process events** (process execution, parent process, command-line arguments).  
  3. **Network events** (outbound connections, remote IPs/ports, DNS lookups).  
  4. **Scheduled Task / Persistence artifacts** (task definitions, registry, etc.).  
  5. **Performance metrics** over time (CPU, GPU usage) if available.

- Ensure chain of custody for any artifacts if legal/compliance is involved.  
- Optionally take forensic images of affected machines if deeper analysis is needed.

---

## Communication & Reporting

- **Internal Stakeholders**: IT leadership, CISO, affected system owners. Give updates on scope, impact, remediation status.  
- **User Notifications**: If users are affected, communicate what happened, what to expect (e.g., performance degradation, possible data loss if misconfigured).  
- **Regulatory / Legal Reporting**: If incident triggers compliance obligations (e.g., data exfiltration discovered or breach), involve Legal / Compliance as soon as possible.  
- **Documentation**: Detailed incident report including timeline, root cause, impact, remediation steps, lessons learned.

---

## Metrics & Postmortem

Track KPIs to evaluate effectiveness:

- Time from detection to containment.  
- Time from containment to full eradication and recovery.  
- Number of affected devices.  
- System performance pre- and post-incident.  
- Number of re-infections (if any).  
- Gaps in detection or response identified in the incident.  

Conduct a postmortem meeting (include SOC, IR, Engineering, Legal) and produce a “Lessons Learned” summary. Update policies and playbooks accordingly.
