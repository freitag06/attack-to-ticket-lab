# Network Correlation

## Timeline

- 08:26:13 - powershell.exe started
- 08:26:13 - whoami.exe spawned by powershell.exe
- 08:26:13 - HOSTNAME.exe spawned by powershell.exe
- 08:26:13 - curl.exe spawned by powershell.exe
- 08:26:14 - TCP connection observed from 10.10.10.20 to 10.10.10.30:443

## Analysis

The sequence shows PowerShell performing basic system discovery and then launching curl.exe. A network connection to the Wazuh server occurred immediately afterward.

The network event did not always contain complete process metadata, so correlation with Process Create events was required.

## Key takeaway

A single event may be incomplete. Correlating process creation and network telemetry provides a more reliable view of host activity.
