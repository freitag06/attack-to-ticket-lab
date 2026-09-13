# PowerShell Discovery Triage

## Alert

Rule: Powershell process spawned powershell instance
Level: 4

## Observed activity

A PowerShell process spawned another Powershell instance with the command:

powershell.exe -NoProfile -Command "whoami; hostname; Get-LocalUser"

## Interpretation

The commands were used to collect information about:

- current user
- hostname
- local user accounts

This behavior may be legitimate administrative activity, but it can also be consistent with post-compromise discovery.

## Initial classification

Suspicious / requires additional context

## Additional checks

- Verify whether the user is an adminstrator or regular employee
- Check whether the activity occurred during expectec working hours
- Review nearby process creation events
- Review network activity before and after the command
- Check whether similar PowerShell usage is normal for the user
- Look for additional discovery or persistence commands

## Conclusion

The alert alone is not enough to confirm malicious activity. More context is required before escalation.
