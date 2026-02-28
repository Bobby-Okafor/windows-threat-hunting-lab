# Windows Threat Hunting Lab

## Overview
Structured, hypothesis-driven threat hunts conducted in a controlled Windows lab environment. Focus: behavioral telemetry correlation across Windows Security Logs and Sysmon to reconstruct multi-stage attack chains and develop KQL-based detection logic.

## Lab Environment
- Single Windows endpoint lab
- Windows Security logging enabled
- Sysmon configured (process creation visibility)
- PowerShell operational logging enabled
- Controlled adversary simulation (PowerShell, Scheduled Tasks, Service creation)

## Methodology
- Hypothesis-driven hunting
- Multi-event correlation and timeline reconstruction
- Execution context validation (logon type, privilege context, parent-child lineage)
- Baseline-informed false-positive reduction
- Structured documentation for analyst handoff

  
## Featured Hunts

- Registry Run Key Persistence  
  → Hunt-RunKey-Persistence/Report.md

- Encoded PowerShell → Scheduled Task Persistence  
  → advanced-powershell-scheduled-task

- Privileged Logon → Service Installation → Follow-on Execution  
  → advanced-service-execution-chain/hunt-report.md

## Detection Development
- 4+ KQL-based detection queries (lab-validated)

## Scope Disclaimer

All hunts were conducted in a controlled lab environment for detection development practice. Queries are conceptual and not deployed in a production SIEM.
