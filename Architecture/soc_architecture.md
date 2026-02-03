## Architecture Foundation For At Home SOC Lab
- Windows 11 VM (Endpoint)
- Kali Linux VM (Attacker)
- Sysmon for endpoint logging
- Splunk Enterprise (SIEM)
- Log forwarding via Splunk Universal Forwarder

---

## Security Use Case Implemented
- Brute force authentication attempts
- Suspicious PowerShell execution
- Unauthorized process creation
- Abnormal login behavior

---

## Detection & Analysis 
For each alert:
- Log source was identified
- Event fields analyzed
- Indicators of compromise (IOCs) reviewe
- False positive vs true positive documentation

---

## Risk & Business Impact
Each detection includes:
-Affected asset 
Potential impact if undetected 
Likelihood and serverity assessment 
Business risk explanation 

---

## Control Mapping 
Detections are mapped to: 
- NIST Cybersecurtiy Framework
- CIS Critical Security Controls

--- 

## Tools Used
-Splunk Enterprise
-Sysmon
-Windows Event Logs
-Kali Linux 

---

##Key Takeaways 
-Improved understanding of SOC workflowd
Experience prioritizing alerts based on risk 
Strengthened ability to translate technical findings into busines impact 
