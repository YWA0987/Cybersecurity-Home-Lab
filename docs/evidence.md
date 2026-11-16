# Screenshot Evidence — Virtualized Cybersecurity Home Lab

These **13 original lab screenshots** were extracted from the Week 1 SOC Analyst and Ethical Hacking setup reports and published without the original report covers or student identifier.

They support the technical claims in the [main README](../README.md), [network configuration](network-configuration.md), and [firewall troubleshooting case study](troubleshooting.md).

| Image | What it demonstrates |
| --- | --- |
| [Kali desktop](../screenshots/kali-desktop.png) | Kali Linux running inside VirtualBox |
| [Windows desktop](../screenshots/windows-desktop.png) | Windows 11 evaluation VM running |
| [Kali VirtualBox network](../screenshots/kali-virtualbox-network.png) | Internal Network selected for Kali |
| [Windows VirtualBox network](../screenshots/windows-virtualbox-network.png) | Matching internal network settings for Windows |
| [Kali static address](../screenshots/kali-static-address.png) | Kali `eth0` using 192.168.50.10/24 |
| [Windows IP configuration](../screenshots/windows-ipconfig.png) | Windows using 192.168.50.20/24 |
| [Initial failed Kali ping](../screenshots/kali-ping-failed.png) | Four transmitted pings with 100% loss |
| [Initial PowerShell access denied](../screenshots/powershell-access-denied.png) | Firewall change blocked by lack of elevation |
| [Successful firewall rule](../screenshots/powershell-firewall-rule.png) | Targeted inbound ICMPv4 rule created in elevated PowerShell |
| [Windows → Kali ping](../screenshots/windows-to-kali-success.png) | Four responses; 0% loss |
| [Kali → Windows ping](../screenshots/kali-to-windows-success.png) | Four responses; 0% loss after firewall adjustment |
| [Kali dual interfaces](../screenshots/kali-dual-interfaces.png) | `eth0` for internal network and `eth1` for NAT |
| [Kali package index update](../screenshots/kali-package-index.png) | Repository connectivity through the NAT interface |

## Evidence highlights

**Firewall troubleshooting — initially blocked inbound ICMP:**

![Kali ping to Windows initially failed](../screenshots/kali-ping-failed.png)

**Successful verification — Kali can reach Windows after creating the rule:**

![Kali to Windows ping succeeded](../screenshots/kali-to-windows-success.png)

**PowerShell — new firewall rule created with administrator privileges:**

![Successful creation of ICMPv4 firewall rule](../screenshots/powershell-firewall-rule.png)

## Notes

- Screenshots are from an **isolated educational lab**, not a production environment.
- The Windows VM displayed an expired evaluation/activation warning; this remains a documented limitation.
- Private lab addresses (192.168.50.0/24) are included for reproducibility. No passwords, VM disks, or original internship report PDFs are published here.
- The screenshots demonstrate **networking, setup and troubleshooting**, not a completed SIEM deployment.
