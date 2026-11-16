# Virtualized Cybersecurity Home Lab

**VirtualBox · Kali Linux · Windows 11 · IPv4 Networking · Windows Firewall**

A growing, hands-on lab for Windows/Linux administration, networking, security monitoring, and investigation practice. This is an **educational environment**, not a production SOC. The initial phase was completed in November 2026 during practical SOC Analyst and Ethical Hacking training.

> **Current status — Phase 1 complete:** Two VMs are running, static IP addresses are configured, and bidirectional ICMP connectivity has been verified. SIEM deployment and incident analysis are **planned**, not completed.

## What I've built

- Deployed a **Kali Linux 2026.3** prebuilt VirtualBox VM and installed a **Windows 11 Enterprise Evaluation** VM from an ISO.
- Configured both guests on a VirtualBox **Internal Network** named **Security-Lab**.
- Manually assigned static IPv4 addresses and checked the subnet configuration on both systems.
- Diagnosed one-way ping failure: Windows reached Kali, but Kali initially could not reach Windows.
- Used elevated PowerShell to create a narrowly scoped **Windows Firewall ICMPv4 inbound rule** rather than disabling the firewall.
- Verified **4/4 successful ICMP replies in both directions** after the change.
- Added a separate **NAT interface to Kali** for package-index downloads while retaining the internal lab interface.

## Environment

| Component | Recorded setup |
| --- | --- |
| Host | Intel Core i7-10700K, 16 GB RAM, SSD |
| Hypervisor | Oracle VirtualBox 7.2.22 |
| Kali Linux VM | 2026.3, prebuilt VirtualBox image, 2 GB RAM, 2 vCPUs |
| Windows VM | Windows 11 Enterprise Evaluation |
| Internal network | Security-Lab, 192.168.50.0/24 |
| Kali internal interface | 192.168.50.10/24 (eth0) |
| Windows internal interface | 192.168.50.20/24 |
| Kali NAT interface | 10.0.3.15/24 (eth1, observed) |

## Network architecture

\`\`\`mermaid
flowchart LR
    W["Windows 11 VM<br/>192.168.50.20/24"]
    K["Kali Linux VM<br/>eth0: 192.168.50.10/24"]
    N["VirtualBox NAT<br/>Kali eth1: 10.0.3.15/24"]
    W <-->|"ICMP: 0% packet loss"| K
    K -. "Package downloads" .-> N
\`\`\`

Both VMs communicate over the isolated **Security-Lab** internal network. Kali also has a *separate* NAT adapter used for software repository access. Intentionally vulnerable practice targets will remain on separate isolated networks without internet-facing adapters.

## Troubleshooting highlight

**Problem:** Windows could ping Kali, but a Kali-to-Windows ping returned **100% packet loss**.

**Investigation:** Checked the network names and static IPs, then tested whether Windows Firewall was filtering inbound ICMP echo requests. The first firewall-rule command returned **Access is denied (System Error 5)** because PowerShell was not elevated.

**Fix:** Restarted PowerShell as administrator and created an inbound ICMPv4 rule restricted to traffic from **192.168.50.10** destined for **192.168.50.20**. Kept Windows Firewall enabled.

**Result:** Verified **four replies out of four** in both directions, with **0% packet loss**.

Read the [detailed troubleshooting case study](docs/troubleshooting.md) and [network configuration](docs/network-configuration.md).

## Portfolio evidence

The screenshots below were extracted and sanitized from my lab reports. They are stored in a separate starter package and will be uploaded to the repository's **screenshots/** folder. See [evidence inventory](docs/evidence.md) for the exact files and what they demonstrate.

## Roadmap

- [x] Deploy Kali and Windows virtual machines
- [x] Configure internal network and static addressing
- [x] Diagnose firewall restrictions and verify bidirectional ICMP
- [x] Configure Kali's separate NAT connection for package updates
- [ ] Analyze Linux and Windows event logs
- [ ] Capture and interpret Wireshark traffic
- [ ] Install Splunk or Wazuh and ingest logs
- [ ] Develop SIEM dashboards, searches, and alerts
- [ ] Investigate a simulated incident and document findings
- [ ] Build a separately isolated, intentionally vulnerable ethical hacking lab

Details: [PROJECT_ROADMAP.md](PROJECT_ROADMAP.md). Completed work will be added in new commits with supporting evidence.

## Limitations and safe use

- The Windows evaluation image displayed an expired evaluation/activation warning. Licensing status needs resolution before continued use.
- These results were produced in **my own virtual lab**; no third-party systems were tested.
- Lab VM images, credentials, private data, and internship reports are not included.
- This repository currently demonstrates virtualized networking and troubleshooting, **not yet** operational SIEM monitoring or incident response.

## Documentation

- [Network configuration](docs/network-configuration.md)
- [Firewall troubleshooting walkthrough](docs/troubleshooting.md)
- [Screenshot inventory](docs/evidence.md)
- [Project roadmap](PROJECT_ROADMAP.md)

**Skills demonstrated:** VirtualBox, Windows, Kali Linux, Linux commands, IPv4 networking, static IPs, ICMP, Windows Firewall, PowerShell elevation, systematic troubleshooting, technical documentation.
