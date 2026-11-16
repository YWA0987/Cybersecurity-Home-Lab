# Case Study: Kali-to-Windows Ping Failure

## Symptom
The **Windows VM could ping the Kali VM**, but the Kali VM's initial attempt to ping Windows resulted in **100% packet loss**.

Lab addresses:
- Kali Linux: **192.168.50.10/24**
- Windows 11: **192.168.50.20/24**
- Shared VirtualBox Internal Network: **Security-Lab**

## Troubleshooting process
1. Checked that both VMs were on the same internal network and subnet.
2. Considered Windows Firewall as the cause of asymmetric inbound ICMP behavior.
3. Attempted to create a targeted inbound firewall rule in PowerShell.
4. Received **Access is denied (System Error 5)** because PowerShell was not running with administrator privileges.
5. Reopened PowerShell using **Run as administrator** and created the rule successfully.
6. Repeated the ping tests in **both directions** to verify the hypothesis.

## Firewall rule

The following illustrates the rule used in my own isolated Windows lab VM. It accepts only **ICMPv4 echo requests (type 8)** from the Kali internal IP to the Windows internal IP. The firewall stayed enabled.

```powershell
New-NetFirewallRule `
  -DisplayName "Security Lab - Ping from Kali" `
  -Direction Inbound `
  -Protocol ICMPv4 `
  -IcmpType 8 `
  -RemoteAddress 192.168.50.10 `
  -LocalAddress 192.168.50.20 `
  -Action Allow `
  -Profile Any
```

The original rule used all profiles, but limited allowed traffic by protocol, ICMP type, source IP, and destination IP.

## Verified outcome

| Direction | Sent | Received | Loss |
| --- | ---: | ---: | ---: |
| Windows → Kali | 4 | 4 | 0% |
| Kali → Windows | 4 | 4 | 0% |

## Lessons learned
- One-way connectivity failure does not necessarily mean both adapters are misconfigured.
- Security controls can filter inbound echo requests.
- Privileged changes must be run in an elevated session; being in a system directory is not sufficient.
- Prefer tightly scoped firewall exceptions to disabling security protections.
- Retest the original problem after applying a potential fix.

**Scope:** These were isolated lab tests, not production security investigations or penetration tests.
