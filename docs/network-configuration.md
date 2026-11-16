# Network Configuration — Phase 1

## Objective
Allow two VirtualBox guests to communicate on a private internal segment while enabling package downloads through a separate Kali network interface.

| Guest | Interface / mode | IPv4 address |
| --- | --- | --- |
| Kali Linux | eth0 / Internal Network: Security-Lab | 192.168.50.10/24 (static) |
| Windows 11 Enterprise Evaluation | Internal Network: Security-Lab | 192.168.50.20/24 (static) |
| Kali Linux | eth1 / NAT | 10.0.3.15/24 (observed) |

Both systems use the **192.168.50.0/24** subnet. Neither default gateway nor DNS was required for their direct IP-address ping tests. The VirtualBox Internal Network does not inherently connect to the host network or internet; Kali's *additional NAT interface* is separate.

## Verification steps

### Kali
```bash
ip -br addr
ping -c 4 192.168.50.20
```

### Windows
```powershell
ipconfig
ping -n 4 192.168.50.10
```

After troubleshooting Windows Firewall, both directions returned four successful replies and **0% packet loss**.

## Practical details
- VirtualBox version recorded: **7.2.22**
- Kali Linux **2026.3** used a prebuilt VirtualBox image: **2 GB RAM, 2 vCPUs**
- Windows 11 Enterprise Evaluation was installed from an ISO
- Host hardware: Intel Core **i7-10700K**, **16 GB DDR4 RAM**, SSD
- CPU virtualization was enabled in the host BIOS before running the guests
- Package index retrieval succeeded from Kali through NAT using `sudo apt update`

## Safety and constraints
Future deliberately vulnerable targets should use their own isolated, non-internet-facing networks. The Windows evaluation image displayed an expired-license warning, which needs resolution before continued use. Never share host credentials or genuine confidential traffic in repository examples.

Related: [Connectivity troubleshooting](troubleshooting.md).
