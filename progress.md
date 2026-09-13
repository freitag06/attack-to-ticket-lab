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
