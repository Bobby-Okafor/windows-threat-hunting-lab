# Advanced Chained Hunt  
## Encoded PowerShell Execution → Scheduled Task Persistence

---

## Objective

Detect multi-stage execution-to-persistence behavior involving encoded PowerShell execution followed by scheduled task creation.

---

## Hypothesis

An adversary may execute PowerShell using Base64-encoded arguments (-enc) to obfuscate intent, then establish persistence via scheduled task creation (Event ID 4698). Correlating process creation telemetry with scheduled task artifacts should expose this chained behavior.

---

## Lab Environment

- Single Windows endpoint
- Windows Security logging enabled
- Sysmon configured (Event ID 1 – Process Creation visibility)
- PowerShell Operational logging enabled
- Controlled adversary simulation

 Controlled lab simulation; not production SIEM deployment. 

---

## Telemetry Sources

| Data Source | Event ID | Purpose |
|-------------|----------|----------|
| Windows Security Log | 4688 | Process creation visibility |
| Windows Security Log | 4698 | Scheduled task creation |
| Sysmon | 1 | Parent-child lineage validation |
| PowerShell Operational Log | 4104 | Script block visibility (if enabled) |

---

## Attack Simulation Summary

1. Executed PowerShell with Base64-encoded argument (-enc).
2. Created scheduled task configured with persistence trigger.
3. Validated resulting telemetry across Security and Sysmon logs.

---

## Behavioral Correlation Logic

1. Identify encoded PowerShell execution (CommandLine contains "-enc").
2. Validate parent-child process lineage via Sysmon.
3. Detect scheduled task creation (Event ID 4698).
4. Correlate timeline proximity between execution and task creation.
5. Validate privilege context and execution attributes.

---

## Detection Logic (Conceptual KQL Structure)

See `detection-query.kql` for full correlation query.

Detection approach:
- Identify encoded PowerShell execution (Event ID 4688).
- Correlate with Event ID 4698 within defined time window.
- Validate execution context.


## Tuning Considerations

- Baseline legitimate encoded PowerShell usage.
- Exclude recurring administrative scheduled tasks.
- Apply time-window constraints to reduce correlation noise.

## Investigation Workflow

1. Decode Base64 payload to assess intent.
2. Inspect scheduled task configuration and execution context.
3. Validate initiating account privilege level.
4. Escalate if persistence tradecraft is confirmed.

## Outcome

## Evidence Artifacts

1. **Task Creation via PowerShell Script**  
   ![Task Creation](Artifacts/01_PowerShell_TaskCreation.png)

2. **PowerShell ScriptBlock Log (4104 GUI)**  
   ![4104 GUI](Artifacts/02_Event4104_GUI.png)

3. **Process Creation Event (4688 GUI)**  
   ![4688 GUI](Artifacts/03_Event4688_GUI.png)

4. **Process Creation Query Results**  
   ![4688 Query](Artifacts/04_Event4688_Query.png)

5. **Scheduled Task Creation Query Results**  
   ![4698 Query](Artifacts/05_Event4698_Query.png)

6. **Alternate Scheduled Task Creation Evidence**  
   ![4698 Query Alt](Artifacts/06_Event4698_Query_Alt.png)

7. **PowerShell ScriptBlock Query Results (4104)**  
   ![4104 Query](Artifacts/07_Event4104_Query.png)

8. **Scheduled Task Creation Event (4698 GUI)**  
   ![4698 GUI](Artifacts/08_Event4698_GUI.png)

9. **Task Execution Confirmation (Event 110)**  
   ![Task Execution](Artifacts/09_Event110_TaskExecution.png)

Established structured multi-event detection logic for identifying execution-to-persistence chaining within Windows telemetry.


