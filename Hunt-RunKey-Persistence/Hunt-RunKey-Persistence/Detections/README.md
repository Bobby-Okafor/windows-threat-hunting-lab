# Detections (KQL)

KQL hunting queries for the Run Key Persistence hunt.

## Files
- `runkey_persistence_sysmon13.kql` — detects HKCU Run key modifications (Sysmon EID 13)
- `runkey_persistence_chain_13_to_4688.kql` — correlates Run key modification to follow-on process creation
