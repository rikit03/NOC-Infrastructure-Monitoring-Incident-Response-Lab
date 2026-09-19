# NOC Infrastructure Monitoring & Incident Response Lab

A hands-on **NOC simulation** demonstrating infrastructure monitoring, Linux administration, SNMP, network troubleshooting, alert investigation, and incident response.

Built from the ground up using **Ubuntu Server, Zabbix, EVE-NG, VMware Workstation Pro, and Wireshark**.

The project emphasizes a practical operational workflow:

**Monitor → Detect → Investigate → Remediate → Verify → Document**

---

## 🎯 Project Overview

The lab simulates a small IT/NOC monitoring environment designed to demonstrate skills relevant to:

* Junior NOC
* IT Support
* Service Desk
* Infrastructure Support
* Network Support

The environment includes a Linux-based Zabbix monitoring server and an EVE-NG network topology for simulated infrastructure monitoring and incident scenarios.

---

## 🏗️ Architecture

```text
                         Windows 11 Host
                      VMware Workstation Pro
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
          Ubuntu Server 24.04             EVE-NG
                 │                      Network Lab
        ┌────────┼────────┐                  │
        │        │        │                  │
        ▼        ▼        ▼                  ▼
     Zabbix    MySQL    Apache          R1 / SW1
        │                                  │
        │                             NOC Hosts
        │
        ▼
   SNMP Monitoring
        │
        ▼
   Metrics & Alerts
        │
        ▼
 Incident Investigation
        │
        ▼
     Wireshark
```

### Management Network

| System     | Address          |
| ---------- | ---------------- |
| Ubuntu-NOC | `192.168.80.131` |
| EVE-NG     | `192.168.80.132` |
| SNMP       | UDP `161`        |

---

## 🛠️ Technology Stack

| Category           | Technologies                 |
| ------------------ | ---------------------------- |
| Operating System   | Ubuntu Server 24.04 LTS      |
| Monitoring         | Zabbix 7.4                   |
| Network Monitoring | SNMP / SNMPv2c               |
| Database           | MySQL                        |
| Web Server         | Apache 2                     |
| Network Simulation | EVE-NG Pro                   |
| Packet Analysis    | Wireshark                    |
| Virtualization     | VMware Workstation Pro       |
| Administration     | SSH, Bash, APT, systemd      |
| Networking         | TCP/IP, DNS, DHCP, UDP, SNMP |

---

# ✅ Completed

## Monitoring Infrastructure

* Deployed **Ubuntu Server 24.04 LTS**
* Configured static network addressing and verified connectivity
* Verified DNS resolution
* Configured SSH remote administration
* Installed and configured **Zabbix Server 7.4**
* Configured **MySQL** database backend
* Configured **Apache** web frontend
* Installed and configured **Zabbix Agent**
* Verified live CPU, memory, and disk monitoring
* Installed and configured **SNMP**
* Verified SNMP daemon operation and UDP/161 listening
* Successfully performed local SNMP polling
* Successfully performed network SNMP polling against `192.168.80.131`

### SNMP Verification

Network polling was successfully verified using:

```bash
snmpwalk -v2c -c public 192.168.80.131 1.3.6.1.2.1.1
```

The response returned system information including:

* System description
* System uptime
* System name
* Standard SNMP system OIDs

---

## EVE-NG Network Lab

* Deployed **EVE-NG Pro 7.2.0-4-PRO**
* Configured virtual networking
* Resolved an initial Bridged/Wi-Fi connectivity problem
* Reconfigured EVE-NG using NAT/DHCP
* Verified EVE-NG web access
* Created the NOC network topology
* Configured the management network
* Added router, switch, and host nodes

### Current Topology

```text
             Cloud0 / Management
                     │
                R1-NOC-Router
                     │
                SW1-NOC-Switch
                  /       \
                 /         \
        NOC-Host01      NOC-Host02
```

---

# 🔧 Real Troubleshooting Performed

The project documents actual troubleshooting performed during deployment.

### Zabbix Environment

**Problem:** Initial Zabbix dependency and database initialization issues.

**Investigation:** Reviewed package compatibility, database configuration, privileges, and schema initialization.

**Resolution:** Rebuilt the monitoring environment on Ubuntu 24.04 LTS and corrected the database configuration/schema import.

---

### EVE-NG Connectivity

**Problem:** EVE-NG was initially unreachable when using Bridged networking over Wi-Fi.

**Investigation:** Tested virtual networking and connectivity between the host and VM.

**Resolution:** Reconfigured the EVE-NG VM using NAT + DHCP and verified web access.

---

### SNMP Network Polling

**Problem:** Remote SNMP polling initially failed.

**Investigation:** Verified the SNMP service and examined its listening sockets and configuration.

The daemon was initially restricted to localhost:

```text
127.0.0.1:161
[::1]:161
```

A conflicting `agentaddress` configuration was identified in:

```text
/etc/snmp/snmpd.conf
```

**Resolution:** Removed the conflicting localhost binding and restarted the SNMP service.

The service was then verified listening on:

```text
0.0.0.0:161
```

Network SNMP polling subsequently succeeded.

### Troubleshooting Method

**Problem → Investigate → Identify Root Cause → Remediate → Verify**

---

# 📊 NOC Monitoring Workflow

The completed environment is being extended into a complete NOC workflow:

```text
Infrastructure
      ↓
SNMP / Monitoring
      ↓
Metrics
      ↓
Alert
      ↓
Triage
      ↓
Investigation
      ↓
Root Cause
      ↓
Remediation
      ↓
Recovery Verification
      ↓
Incident Documentation
```

---

# 🚨 Incident Response Scenarios

The next phase will demonstrate simulated NOC incidents including:

* Host/device unavailable
* Packet loss
* High CPU utilization
* High memory utilization
* Interface failure
* DNS failure
* DHCP failure
* SNMP service failure
* Service availability failure

Where appropriate, **Wireshark** will be used to collect packet-level evidence during investigation.

Each incident will be documented using:

```text
Detection
   ↓
Triage
   ↓
Investigation
   ↓
Root Cause
   ↓
Remediation
   ↓
Verification
   ↓
Documentation
```

---

# 📸 Project Evidence

Current evidence includes:

1. **Ubuntu network configuration**
2. **SSH service verification**
3. **SNMP service verification**
4. **Zabbix dashboard**
5. **Live Zabbix host monitoring**
6. **EVE-NG web interface**
7. **EVE-NG NOC topology**
8. **Successful network SNMP polling**

Additional evidence will document Zabbix SNMP monitoring, alerts, incident investigation, Wireshark traffic, and recovery.

---

# 🧠 Skills Demonstrated

### Linux / Systems

* Ubuntu Server administration
* Bash
* APT
* systemd
* SSH
* Linux networking
* Service troubleshooting

### Monitoring

* Zabbix Server
* Zabbix Agent
* Host monitoring
* Resource monitoring
* SNMP
* SNMP polling
* Monitoring architecture
* Alert investigation

### Networking

* TCP/IP
* DNS
* DHCP
* UDP
* SNMP
* Connectivity troubleshooting
* Virtual networking
* EVE-NG

### Infrastructure

* VMware Workstation Pro
* EVE-NG
* Linux server deployment
* NAT/DHCP
* Virtual network environments

### Troubleshooting

* Root-cause analysis
* Fault isolation
* Service troubleshooting
* Network troubleshooting
* Configuration analysis
* Technical evidence collection
* Incident documentation

---

# 📈 Project Progress

### Infrastructure Foundation

* [x] Ubuntu Server 24.04 LTS
* [x] Network configuration
* [x] DNS/connectivity verification
* [x] SSH
* [x] Zabbix Server
* [x] MySQL
* [x] Apache
* [x] Zabbix Agent
* [x] Live system monitoring
* [x] SNMP installation
* [x] SNMP configuration
* [x] Local SNMP polling
* [x] Network SNMP polling

### EVE-NG Environment

* [x] EVE-NG deployment
* [x] Virtual networking
* [x] Management network
* [x] NOC topology
* [x] Router/switch/host nodes

### NOC Monitoring & Incident Response

* [ ] Add SNMP-monitored host(s) to Zabbix
* [ ] Verify SNMP metrics in Zabbix
* [ ] Configure monitoring triggers
* [ ] Generate monitoring alerts/problems
* [ ] Simulate NOC incidents
* [ ] Investigate incidents
* [ ] Capture Wireshark evidence
* [ ] Remediate incidents
* [ ] Verify recovery
* [ ] Produce incident reports
* [ ] Finalize project documentation

---

# 💼 Project Value

This project demonstrates practical experience with the same general workflow used in entry-level IT operations and NOC environments:

**Monitoring → Alert Triage → Troubleshooting → Root Cause Analysis → Remediation → Verification → Documentation**

Rather than demonstrating only software installation, the lab focuses on **hands-on infrastructure operations, troubleshooting, monitoring, and incident-response processes**.

---

# 👨‍💻 About

**Rikit Thapa**

Computer Systems Networking Technician — Loyalist College
Dean's List

**Career Focus:** IT Support · Service Desk · Junior NOC · Infrastructure Support

### Other Hands-On Projects

* [Windows IT Support & Active Directory Lab](#)
* [Cisco Campus Network Design](#)
* [IT Service Desk & Incident Management Lab](#)
* **NOC Infrastructure Monitoring & Incident Response Lab**

---

## 📌 Project Status

**🟡 In Progress**

### Current Completion: ~70%

**Completed:**

Ubuntu monitoring infrastructure, Zabbix foundation, Linux administration, SNMP configuration and verification, EVE-NG deployment, virtual networking, and NOC topology.

**Current Phase:**

Zabbix SNMP monitoring integration.

**Remaining:**

```text
Zabbix SNMP Monitoring
        ↓
Live SNMP Metrics
        ↓
Alerts / Problems
        ↓
Incident Simulation
        ↓
Investigation
        ↓
Wireshark Evidence
        ↓
Remediation
        ↓
Recovery Verification
        ↓
Incident Reports
```

The project is being developed incrementally with screenshots and technical evidence documenting the implementation and troubleshooting process.
