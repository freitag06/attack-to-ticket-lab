## Day 1

### Completed

- Installed VirtualBox
- Downloaded Kali Linux VM image
- Downloaded Ubuntu Server ISO
- Verified the Kali Linux image using SHA-256

### Learned

- Understood the difference between a host system and a guest virtual machine
- Understood why virtual machines are useful for safe cybersecurity labs
- Learned how SHA-256 can be used to verify file integrity
- Gained a basic understanding of NAT and why a virtual machine can have a different IP address than the host
- Learned that the home router does not necessarily see a NAT-based virtual machine as a separate device

### Time

~60 min

### Key takeaway

A virtual machine behaves like a separate computer with its own operating system and network interface, while still using the physical resources of the host.

## Day 2

### Completed

- Added an isolated internal network to Kali
- Configured a static lab IP address
- Verified Internet access through NAT
- Inspected Linux network interfaces and routing table

### Learned

- Difference between NAT and Internal Network
- What a network interface is
- Basic meaning of IP address and /24 subnet
- Purpose of a default gateway
- Basic routing table interpretation

### Key takeaway

Kali uses two separate network interfaces: `eth0` provides Internet access through NAT, while `eth1` is used for communication inside the isolated LAB-NET. Traffic to devices in the same subnet, such as `10.10.10.20`, does not need to pass through the default gateway.

### Additional completed

- Created Windows 11 victim VM
- Assigned static ip 10.10.10.20/24
- Verified bidirectional connectivity between Kali and Windows victim

### Key Takeaway

Devices in the same subnet communicates directly with each other. Kali sends traffic to 10.10.10.20 through eth1 because the routing table associates 10.10.10.0/24 with the LAB-NET interface.

## Day 3

### Completed

- Created Ubuntu Server VM for Wazuh
- Configured Ubuntu in LAB-NET as 10.10.10.30/24
- Verified connectivity between Kali, Windows victim and Ubuntu
- Configured and tested SSH
- Installed Wazuh all-in-one
- Verified Wazuh Manager, Indexer and Dashboard
- Installed Wazuh Agent on Windows victim
- Connected Windows victim to Wazuh Manager
- Installed Sysmon on Windows
- Configured Wazuh Agent to collect Sysmon events
- Verified Sysmon Event ID 1 in Wazuh
- Performed first PowerShell discovery test
- Completed first basic SOC alert triage

### Learned

- Difference between a host, service and port
- Basic SSH and Linux service management
- How Wazuh components work together
- Difference between an event and an alert
- Role of Wazuh Agent
- Role of Sysmon as a telemetry source
- Windows process creation telemetry
- Meaning of Image, CommandLine and ParentImage
- Basic SOC alert triage and contextual investigation

### Key takeaway

Security monitoring is a pipeline. Sysmon generates endpoint telemetry, Windows stores it in Event Logs, Wazuh Agent collects it, Wazuh Manager analyzes it using detection rules, and the analyst investigates the resulting events and alerts in the dashboard.

An alert alone does not prove malicious activity. Context is required to determine whether activity is benign, suspicious or malicious.

## Day 4

### Completed

- Enabled Sysmon network connection logging
- Generated controlled network traffic from Windows victim to Wazuh
- Collected and analyzed Sysmon Event ID 1 and Event ID 3
- Correlated process creation events with network activity
- Built the first event timeline
- Investigated incomplete telemetry where Sysmon reported `<unknown process>`
- Used ProcessId and timestamps to correlate related events

### Learned

- Difference between process creation telemetry and network connection telemetry
- Sysmon Event ID 1 represents process creation
- Sysmon Event ID 3 represents network connections
- How ProcessId, ProcessGuid and timestamps can be used for event correlation
- Why a single log entry may not provide enough context
- How to reconstruct a sequence of activity from multiple events
- Why PowerShell activity must be evaluated in context rather than automatically classified as malicious
- How source IP, destination IP, destination port and transport protocol describe network activity

### Timeline

- 08:26:13 - powershell.exe started
- 08:26:13 - whoami.exe spawned by powershell.exe
- 08:26:13 - HOSTNAME.exe spawned by powershell.exe
- 08:26:13 - curl.exe spawned by powershell.exe
- 08:26:14 - TCP connection observed from 10.10.10.20 to 10.10.10.30:443

### Analysis

The sequence shows PowerShell performing basic host and user discovery before launching curl.exe. Immediately afterwards, the Windows victim established a TCP connection to the Wazuh server on port 443.

The network event did not contain complete process metadata and reported an unknown process. Correlation with nearby process creation events was therefore required to reconstruct the activity.

This sequence is not proof of malicious activity, but it demonstrates behavior that could require further investigation in a real SOC environment.

### Key takeaway

Individual events can be incomplete or ambiguous. Correlating process, user, command-line and network telemetry produces a much more reliable picture of what happened on an endpoint.

## Day 5

### Completed

- Executed a controlled discovery sequence on the Windows victim
- Collected related Sysmon process creation events
- Reviewed the same activity in Wazuh Threat Hunting
- Identified the purpose of each discovery command
- Mapped observed behavior to MITRE ATT&CK techniques
- Compared benign administrative use with suspicious use
- Created the first MITRE discovery chain for the lab

### Discovery chain

- `whoami` → T1033 – System Owner/User Discovery
- `hostname` → T1082 – System Information Discovery
- `Get-LocalUser` → T1087.001 – Account Discovery: Local Account
- `ipconfig` → T1016 – System Network Configuration Discovery
- `Get-NetTCPConnection` → T1049 – System Network Connections Discovery

### Learned

- Difference between MITRE ATT&CK tactics and techniques
- How normal system commands can represent attacker behavior depending on context
- Why a single discovery command is usually weak evidence
- Why several discovery actions executed close together can form a stronger behavioral pattern
- How command-line context, parent process, user, timing and network activity influence triage
- How ATT&CK provides a common language for describing observed behavior
- How MITRE ATT&CK can support detection engineering and coverage analysis
- Difference between an external executable and a PowerShell cmdlet executed inside an existing PowerShell process

### Key takeaway

Individual commands such as `whoami` or `ipconfig` are not malicious by themselves. Their analytical value increases when they are correlated with other discovery activity, unusual users, suspicious parent processes or network behavior.

MITRE ATT&CK helps translate raw commands and events into structured attacker behavior that can be used during investigation and detection engineering.

### Time

~60 min
