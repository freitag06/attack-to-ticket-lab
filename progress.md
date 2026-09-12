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
