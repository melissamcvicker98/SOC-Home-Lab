# Network Connectivity Validation

## Objective
Verify network connectivity between Kali Linux and Windows endpoint to support attack simulation and log generation.

## Environment
- Kali Linux (attacker system)
- Windows 10 (monitored endpoint)
- VirtualBox NAT Network

## Procedure
1. Identified the Windows IPv4 address using `ipconfig`.
2. Executed an ICMP ping test from Kali Linux to the Windows endpoint.
3. Observed successful ICMP responses.

## Result
Network connectivity was successfully established between Kali Linux and the Windows endpoint.

##Evidence
## Evidence
![Successful ping from Kali to Windows](../images/ping success 1.png)

