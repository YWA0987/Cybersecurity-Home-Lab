# Cybersecurity Home Lab — Project Roadmap

This is a **living checklist**, not a list of completed experience. Each future item will be marked complete only after the practical exercise is performed, checked, and documented.

## Phase 1: Virtualization and networking — COMPLETE
- [x] Deploy Kali Linux and Windows 11 as separate VirtualBox guests
- [x] Configure the Security-Lab internal network
- [x] Assign static addresses in the 192.168.50.0/24 subnet
- [x] Troubleshoot Windows Firewall ICMP filtering
- [x] Verify bidirectional connectivity with 0% packet loss
- [x] Add a separate NAT adapter to Kali for package-list updates

## Phase 2: OS logs — IN PROGRESS
- [x] Explore Linux logs under /var/log
- [x] Read plain-text logs with cat, less, tail, and grep
- [x] Use journalctl when expected auth.log and syslog files are absent
- [x] Search the current journal for a local sudo authentication failure
- [ ] Use Windows Event Viewer to inspect relevant security and system events
- [x] Generate a safe local journal event with logger and verify it in journalctl -f

Linux portion documented on November 18, 2026: [walkthrough and screenshots](docs/linux-log-analysis.md). Windows Event Viewer work remains pending.

## Phase 3: Wireshark — PLANNED
- [ ] Capture traffic generated between controlled lab systems
- [ ] Identify protocols, source and destination IP addresses, and relevant packet details
- [ ] Publish sanitized screenshots or synthesized examples

## Phase 4: SIEM deployment — PLANNED
- [ ] Choose Splunk or Wazuh and review resource requirements for a 16 GB host
- [ ] Install/configure the SIEM
- [ ] Ingest Windows/Linux logs and verify event arrival
- [ ] Create and test dashboards and alerts

## Phase 5: Security investigation — PLANNED
- [ ] Investigate suspicious activity from a controlled lab exercise or shareable dataset
- [ ] Document evidence, timeline, reasoning, and uncertainty
- [ ] Write a professional incident report with suggested mitigations

## Optional ethical hacking track — PLANNED
- [ ] Create a separate isolated network for deliberately vulnerable systems
- [ ] Establish authorized targets and scope
- [ ] Perform controlled reconnaissance and web application testing
- [ ] Publish sanitized findings, risk descriptions, and remediation guidance

## Update process
For each milestone: run the lab, collect safe evidence, add a dedicated document in docs/, update the main README, and commit a descriptive change. Do not publish passwords, tokens, private traffic, virtual machine disks, or proprietary training materials.
