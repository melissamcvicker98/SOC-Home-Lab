### SOC Home Lab - Networking 
---

## Purpose 
This folder documents the networking design for my SOC home lab, including segmentation, traffic flows, and the network telemetry I collect to support detection and investigation 

---

## Lab Network Overview 
Goals:
- Separate attacker and victim systems for safe testing
- Allow controlled attack simulation without exposing services publicly 
- Control and observe east-west traffic between VMs
- Enable log collection to my SIEM (Splunk) without exposing services publicly

---

## Environment 
- Hypervisor: VMware
- Network Mode: NAT
- Host OS: Windows
- SIEM: Splunk Enterprise 
- Key VMs:
  - Windows 11 (Victim / Endpoint
  - Kali Linux (Attacker)
  - Splunk Server: SIEM and log analysis
 
---

## Network Topology 
Network Type: 
- NAT
  -Why did I choose NAT?
      - VMs easily able to communicate (interal VM-to-VM communication)
      - Isolated networking and security as it acts as a virtual firewall
  
---

## Traffic Flows 
Allowed flows: 
- Windows 11 --> Splunk Server
    - TCP 9997
    - Purpose: Forwarding logs via Splunk Universal Forwarder
- Admin Access
    - Splunk Web UI (TCP 8000) from host browser
 - Controlled Testing
    - Kali Linux --> Windows 11 (only during testing)

Block / Restricted flows: 
- No inbound connections from external networks
- No direct exposure of Splunk ingestion ports to the internet
- Attacker traffic limited to lab scope only

---

### Network Telemetry Collected 
## Splunk Inputs
- Forwarder port: TCP 9997
- Splunk Web: 8000
- Data sources (related to networking)
  - Sysmon Event ID 3 - Network connections
  - Sysmon Event ID 22 - DNS queries 
  - Windows Security Logs (when enabled)

## Why this telemetry matters:
- Detect suspicious outbound connections
- Identification of unusual ports or destinations
- Identify lateral movement attempts
- Correlate endpoint processes to network activity 

---

### Configuration Notes 
## IP Addressing 
- IPs assigned dynamically via VMware NAT
- All VMs share the same private subnet
- No static IPs required for lab functionality
## Splunk Forwarder Configuration 
- Forwarder installed on Windows 11 endpoint
- Configured to send logs to Splunk on TCP 9997
- Connectivity validated using: Test-NetConnection <splunk_ip> -Port 9997

---

### Validation and Testing 
Connectivity Verification 
- Confirmed Windows 11 can reach Splunk on port 9997
- Verified log ingestion in Splunk index
- Confirmed Sysmon network events are searchable

 Test Traffic Generated 
- Web browsing
- DNS lookups
- Software downloads
- Port scanning from Kali Linux
- Suspicious outbound connections
- Command execution tied to network activity

---

### Future Improvements 
- Introduce pfSense for segmented internal networks
- Add network IDS
- Build netowrk-based detection rules in Splunk

---

### Why This Matters in a SOC Role
Understanding network architecture and traffic is critcal for: 
- Identifying malicious communication
- Supporting incident repsonse investigations
- Designing effective detections
- Explaining findings to stakeholders
This lab demonstates pratical SOC networking knowledge in a controlled environment 


