# 🔐 Mini SOC – Windows Log Monitoring & Threat Detection with Splunk

A hands-on **Security Operations Center (SOC) lab project** focused on collecting Windows security logs, monitoring events with Splunk, creating security detections, investigating suspicious activity, and building a simple SOC dashboard.

## 🎯 Project Overview

The goal of this project is to understand how a SOC analyst works with Windows security events from collection to investigation.

The project follows a simple SOC workflow:

**Windows Logs → SIEM → Detection → Alert → Investigation → Decision**

The lab uses a Windows virtual machine to generate security events and Splunk to collect, search, analyze, and visualize those events.

## 🛠️ Tools & Technologies

* 🪟 Windows Virtual Machine
* 👁️ Windows Event Viewer
* 🔎 Splunk Enterprise
* 📡 Splunk Universal Forwarder
* 📝 Splunk Search Processing Language (SPL)
* 🎯 MITRE ATT&CK concepts
* 🛡️ SOC investigation methodology

## 🏗️ Project Phases

### Phase 1 – Windows Lab Setup

Created a Windows virtual machine using VirtualBox as the environment for generating and investigating security events.

### Phase 2 – Windows Event Viewer

Learned how to monitor Windows Security logs and understand important Event IDs:

| Event ID | Description                                  |
| -------- | -------------------------------------------- |
| 4624     | Successful Logon                             |
| 4625     | Failed Logon                                 |
| 4720     | User Account Created                         |
| 4722     | User Account Enabled                         |
| 4726     | User Account Deleted                         |
| 4732     | Member Added to Local Security-Enabled Group |
| 4688     | New Process Created                          |

## 🔎 Security Detections

### 1. Failed Login Detection – Event ID 4625

Generated failed login attempts by entering an incorrect password and investigated the resulting Windows Security event.

Example SPL:

```spl
index="main" EventCode=4625
```

Repeated failed login attempts were investigated as potentially suspicious authentication behavior or possible brute-force activity.

### 2. New User Account Detection – Event ID 4720

Created a test Windows account and monitored the resulting Event ID 4720.

The investigation focused on:

* Who created the account?
* What account was created?
* When was it created?
* Which computer was involved?
* Was the account creation authorized?

### 3. Administrator Group Modification – Event ID 4732

Added a test account to the local Administrators group and monitored Event ID 4732.

Example SPL:

```spl
index=* EventCode=4732 Group_Name="Administrators"
| table _time host Subject_Account_Name Member_Security_ID Group_Name
```

This detection is important because unauthorized administrator-group changes can potentially indicate privilege escalation or persistence.

### 4. PowerShell / Process Creation – Event ID 4688

Enabled process creation auditing and monitored Event ID 4688.

During investigation, the following information was considered:

* Account name
* Process name
* Timestamp
* Host
* Command line
* Parent process
* Reason for execution

An important SOC principle demonstrated in this detection is:

> PowerShell activity is not automatically malicious. Context is required to determine whether the activity is legitimate or suspicious.

## 📊 Splunk SOC Dashboard

Built a basic SOC dashboard containing panels for:

* Failed Logins
* Successful Logins
* New Users
* Administrator Group Changes
* PowerShell Events
* Total Windows Events

This dashboard provides a simple view of Windows security activity and helps an analyst identify events that require further investigation.

## 🧠 Key SOC Investigation Questions

Throughout the project, the investigation process focused on questions such as:

**WHO?**
Which account performed the action?

**WHAT?**
What activity occurred?

**WHEN?**
When did the event happen?

**WHERE?**
Which system or host was involved?

**HOW?**
How did the activity occur?

**WHY?**
Was the activity expected, authorized, suspicious, or potentially malicious?

## 🎓 Key Learning Outcomes

Through this project, I gained practical experience with:

* Windows Security Event Logs
* Event IDs and their meanings
* SIEM fundamentals
* Splunk Enterprise
* Splunk Universal Forwarder
* SPL queries
* Security event investigation
* Authentication monitoring
* Account monitoring
* Privilege/group-change monitoring
* Process and PowerShell monitoring
* SOC dashboards
* Basic threat detection
* MITRE ATT&CK concepts

## 🚀 Project Takeaway

This project helped me understand that SOC monitoring is not simply about finding an alert.

A security analyst needs to:

**Collect → Detect → Investigate → Understand Context → Decide**

The project provided hands-on exposure to how Windows security events can be turned into useful SOC detections and investigated using a SIEM platform.

## 📌 Disclaimer

This project was created as a **controlled cybersecurity lab for educational and learning purposes**. Test accounts and security events were generated inside the lab environment.

#CyberSecurity #SOC #Splunk #SIEM #ThreatDetection #BlueTeam #WindowsSecurity #SOCAnalyst #CyberDefense #MITREATTACK
