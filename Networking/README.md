### SOC Home Lab - Networking 
---

## Purpose 
This folder documents the networking design for my SOC home lab, including segmentation, traffic flows, and the network telemetry I collect to support detection and investigation 

---

## Lab Network Overview 
Goals:
- Separate attacker and victim systems for safe testing 
- Control and observe east-west traffic between VMs
- Enable log collection to my SIEM (Splunk) without exposing services publicly

---

## Environment 
- Hypervisor: VMware
- Host OS: Windows
- Key VMs:
  - Windows 11 (Victim / Endpoint) --> 
  - Kali Linux (Attacker) --> 
  - Splunk Server (SIEM) -->
 
---

## Network Topology 
Network Type: 
- NAT
  -Why did I choose NAT?
      - VMs easily able to communicate
      - Isolated networking and security as it acts as a virtual firewall

---

## Traffic Flows 
Allowed flows: 
- Windows 11 --> Splunk (Universal Forwarder --> Splunk on Port 9997)
- Admin / Management:
- Kali Linux --> Windows 11 (only during testing)

Block / Restricted flows: 
- Example: *****
- Example: *****

---

### Network Telemetry Collected 
## Splunk Inputs
- Forwarder port: 9997
- Splunk Web: 8000
- Data sources ingested (related to networking)
  - Sysmon Events IDs realted to network: 3 (Network Connection), 22 (DNS)
  - Windows Security Logs

## Why this telemetry matters:
- Detect suspicious outbound connections (C2, unusual ports)
- Identify lateral movement (SMB/RDP/WinRM patterns)
- Correlate endpoint processes to network connections (Sysmon 3 + process lineage)

---

### Configuration Notes 
## IP Addressing 
- Splunk: IP Address
- Windows 11: IP Address
- Kali Linux: IP Address
- Gateway/DNS: IP Address


