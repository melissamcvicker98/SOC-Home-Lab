# Ports & Services — SOC Home Lab (VMware NAT)

## Purpose
This document lists the key ports and services used in my SOC home lab, explains why each port is needed, and notes security considerations. The lab uses **VMware NAT**, which keeps VMs on a private virtual subnet while allowing outbound internet access.

---

## Scope & Assumptions
- VMs are on a **VMware NAT** network (private subnet)
- Splunk receives logs from the Windows endpoint via **Splunk Universal Forwarder**
- All “attacker” activity (Kali) is restricted to the lab environment

---

## Key Services (Core Lab)

| System | Service | Port/Proto | Direction | Used For | Notes / Hardening |
|---|---|---:|---|---|---|
| Splunk Server | Splunk Web UI | 8000/TCP | Host → Splunk | Access dashboards/search in browser | Restrict access to host-only if possible; strong creds; keep patched |
| Splunk Server | Splunk Receiving (Indexer/Listener) | 9997/TCP | Win11 → Splunk | Ingest logs from Universal Forwarder | Allow only from Win11 IP; verify UF uses TLS if configured |
| Splunk Server (optional) | Splunk Management | 8089/TCP | Admin → Splunk | API/management tasks (some apps/UF mgmt) | If not needed, don’t expose; restrict to admin host/IP only |

---

## Endpoint & Admin Services (As Needed)

| System | Service | Port/Proto | Direction | Used For | Notes / Hardening |
|---|---|---:|---|---|---|
| Windows 11 | RDP (optional) | 3389/TCP | Host → Win11 | Remote admin | Disable if not needed; require NLA; strong password; lockout policy |
| Kali Linux | SSH (optional) | 22/TCP | Host → Kali | Remote admin | Use keys; disable password auth; only enable when needed |
| Any VM | ICMP | ICMP | VM ↔ VM | Basic connectivity testing | Can block once stable; keep for troubleshooting if desired |

---

## Typical “Background” Network Ports (Expected)

These ports are normally used by the OS for standard operations. You’ll often see them in logs and shouldn’t treat them as suspicious by default.

| Category | Port/Proto | Examples |
|---|---:|---|
| DNS | 53/UDP (sometimes TCP) | Name resolution for updates, web browsing |
| HTTP/HTTPS | 80/TCP, 443/TCP | Updates, package downloads, browsing |
| NTP | 123/UDP | Time sync (important for log correlation) |
| DHCP | 67/UDP, 68/UDP | NAT network addressing (VMware-managed) |

---

## Notes on VMware NAT
**What NAT does well**
- VMs can reach the internet (outbound)
- External devices generally cannot initiate inbound connections to VMs
- Great for safe labs and repeatable configs

**Trade-offs**
- Less realistic than segmented VLANs (everything often shares one NAT segment)
- Harder to simulate certain internal network scenarios without extra networks

---

## “Must Be Open” Minimum Ports (Lab Baseline)
If I had to reduce to the essentials:
- **Splunk Web UI:** 8000/TCP (host access)
- **Splunk Receiving:** 9997/TCP (Win11 → Splunk)

Everything else can be optional depending on how you administer the VMs.

---

## Security Controls Implemented / Planned
- Keep services minimal: only enable what the lab needs
- Restrict 9997/TCP to the Windows endpoint only
- Strong authentication on Splunk
- Patch VMs regularly
- (Planned) TLS on forwarder → Splunk ingestion
- (Planned) Add segmentation (pfSense) for “attacker” vs “endpoint” networks

---

## Validation Checklist
- [ ] From Windows 11: `Test-NetConnection <splunk_ip> -Port 9997`
- [ ] In Splunk: confirm data is arriving (search recent events)
- [ ] Validate Sysmon network events are present:
  - `index=main EventCode=3`
  - `index=main EventCode=22`
