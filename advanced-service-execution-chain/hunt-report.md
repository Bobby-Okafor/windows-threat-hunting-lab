# Advanced Chained Hunt  
## Privileged Logon → Service Installation → Follow-on Execution

---

## Objective

Detect service-based remote execution behavior by correlating privileged logon activity with service installation and subsequent process execution.

---

## Hypothesis

An adversary may authenticate remotely using valid credentials (Event ID 4624), receive elevated privileges (Event ID 4672), install a service (Event ID 7045), and trigger process execution (Event ID 4688). Correlating these events within a defined timeline should expose service-based lateral movement patterns.

---

## Lab Environment

- Single Windows endpoint
- Windows Security logging enabled
- Sysmon configured (Event ID 1 – Process Creation visibility)
- Controlled PsExec simulation for service-based execution

Controlled lab simulation; not production SIEM deployment.

---

## Telemetry Sources

| Data Source | Event ID | Purpose |
|-------------|----------|----------|
| Windows Security Log | 4624 | Logon activity |
| Windows Security Log | 4672 | Special privileges assigned |
| Windows Security Log | 4688 | Process creation |
| Windows System Log | 7045 | Service installation |
| Sysmon | 1 | Parent-child process validation |

---

## Attack Simulation Summary

1. Simulated PsExec remote authentication.
2. Observed privileged logon (4624 + 4672).
3. Installed service (7045).
4. Validated resulting process execution (4688).

---

## Behavioral Correlation Logic

1. Identify remote logon activity (Event ID 4624).
2. Confirm special privileges assignment (Event ID 4672).
3. Detect service installation (Event ID 7045).
4. Correlate with process execution telemetry (4688 / Sysmon 1).
5. Validate timeline proximity across events.

---

## Detection Logic

See `detection-query.kql` for full correlation query.

Detection approach:
- Detect privileged remote logon events.
- Correlate service installation events on same host.
- Validate subsequent process execution within defined time window.
- Flag abnormal service creation aligned with elevated authentication context.

---

## Tuning Considerations

- Baseline legitimate administrative service installations.
- Exclude known management tools (if present in environment).
- Validate logon type to distinguish interactive vs remote sessions.
- Apply strict time-window constraints to reduce noise.

---

## Investigation Workflow

1. Validate logon type and source IP address.
2. Confirm privilege elevation context.
3. Inspect installed service binary path and name.
4. Review associated process execution lineage.
5. Escalate if indicators align with unauthorized lateral movement.

---

## Outcome

Established structured detection methodology for identifying service-based execution chains through multi-event telemetry correlation and timeline reconstruction.
