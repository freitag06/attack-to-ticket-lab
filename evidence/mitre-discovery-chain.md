## whoami

→ `T1033 System Owner/User Discovery`

## hostname

→ `T1082 System Information Discovery`

## Get-LocalUser

→ `T1087.001 Account Discovery: Local Account`

## ipconfig

→ `T1016 System Network Configuration Discovery`

## Get-NetTCPConnection

→ `T1049 System Network Connections Discovery`

Command:
hostname

Purpose:
Determine the hostname of the current system.

Why could an attacker use it?
To identify which host has been compromised and use that information during further discovery or lateral movement.

Benign explanation:
A user or administrator may check the hostname during troubleshooting or system administration.

What would make it more suspicious?
Execution together with other discovery commands in a short time window.

MITRE ATT&CK:
T1082 – System Information Discovery

Command:
Get-NetTCPConnection

Purpose:
Display active TCP connections, listening ports and related network endpoints.

Why could an attacker use it?
To understand which systems the host is communicating with, which ports are active and what network services may be available.

Benign explanation:
An administrator may use it while troubleshooting connectivity or checking whether a port is already in use.

What would make it more suspicious?
Execution as part of a broader discovery sequence, especially if followed by unusual outbound connections, scanning or lateral movement activity.

MITRE ATT&CK:
T1049 – System Network Connections Discovery

Command:
ipconfig

Purpose:
Display the system's network configuration.

Why could an attacker use it?
To learn the device's IP address, subnet, gateway and network interfaces, which can help understand the local network environment.

Benign explanation:
An administrator may use it while troubleshooting network connectivity.

What would make it more suspicious?
Execution as part of a broader discovery sequence, especially followed by network scanning, remote connections or other reconnaissance activity.

MITRE ATT&CK:
T1016 – System Network Configuration Discovery

Command:
Get-LocalUser

Purpose:
List local user accounts on the device.

Why could an attacker use it?
To identify available local accounts, disabled/enabled users and potential accounts of interest.

Benign explanation:
An administrator may use it during account management or troubleshooting.

What would make it more suspicious?
Execution together with other discovery commands, account manipulation, privilege checks, or unusual network activity.

MITRE ATT&CK:
T1087.001 – Account Discovery: Local Account

Command:
whoami

Purpose:
Identify the currently logged-in user.

Why could an attacker use it?
To determine which account is currently being used and understand the current user context.

Benign explanation:
An administrator may use it to confirm which account is active in the current session.

What would make it more suspicious?
Execution together with other discovery commands in a short period of time, especially from an unusual parent process or user context.

MITRE ATT&CK:
T1033 – System Owner/User Discovery
