# Sysmon Installation & Configuration (SOC Home Lab)

## 📌 Objective
Deploy Microsoft Sysmon on a Windows endpoint to collect high-fidelity host-based telemetry (process creation, network connections, file creation, and more) as part of a Security Operations Center (SOC) home lab.

---

## 🛠️ Tools & Technologies
- **Operating System:** Windows 11 (Virtual Machine)
- **Monitoring Tool:** Sysmon (Sysinternals)
- **Configuration:** Olaf Hartong Sysmon Modular Configuration
- **Shell:** Windows PowerShell (Administrator)

---

## 📂 Lab Environment
- **Host:** Windows VM
- **Directory:** `C:\Sysmon`
- **Sysmon Version:** v15.15
- **Schema Version:** 4.90

---

## ⚙️ Installation Steps

### 1. Create Sysmon Directory
```powershell
mkdir C:\Sysmon

### 2. Download Sysmon
--Downloaded Sysmon from Microsoft Sysinternals
--Extracted files into C:\Sysmon

### 3. Obtain Sysmon XML Configuration
**Ran into browser file-type handling issues, so the configuratiion was downloaded directly using PowerShell
--PowerShell code used: Invoke-WebRequest -Uri https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig.xml -OutFile C:\Sysmon\sysmonconfig.xml

### 4. Installed Sysmon as Admin
--PowerShell was launched as Administrator and the following code was used to install the Sysmon service and driver:
cd C:\Sysmon
.\Sysmon64.exe -accepteula -i sysmonconfig.xml

### 5. Validation and Verification
--Confirmed the Sysmon Service Status from the following code:
Get-Service Sysmon*
--Result from code:
Status   Name        DisplayName
Running  Sysmon64    Sysmon64
--Generated Test Activity using the following code:
notepad.exe
calc.exe
ping 8.8.8.8
--Verified Event Logs by nabigating to Event Viewer --> Applications and Services Logs --> Microsoft --> Windows --> Sysmon --> Operational
--Events Observed--
Event ID 1: Process Creation (image attached)
Event ID 3: Network Connection (image attached)


