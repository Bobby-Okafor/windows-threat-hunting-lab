# Run Key Persistence Detection Hunt

This hunt focused on identifying persistence established through modification of the HKCU Run registry key originating from a user context.

The investigation tracked:

- Registry value creation via Sysmon Event ID 13  
- Execution triggered through user login context  
- Parent-child lineage showing explorer.exe spawning cmd.exe  
- Delayed payload execution from autorun mechanism  
- Confirmation of persistence via registry enumeration  
- Validation through file output artifacts

The analysis emphasized behavioral detection of autorun-based persistence rather than reliance on static indicators.

Artifacts included demonstrate:

- Registry modification activity  
- Process execution lineage  
- Delayed execution behavior  
- Persistence verification
