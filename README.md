# NOC Infrastructure Monitoring & Incident Response Lab

A hands-on **NOC simulation** designed to demonstrate practical experience in **infrastructure monitoring, Linux administration, SNMP, network troubleshooting, virtual networking, and incident response**.

The environment is being built end-to-end using **Ubuntu Server 24.04 LTS, Zabbix 7.4, EVE-NG, VMware Workstation Pro, and Wireshark**.

The project follows a practical NOC workflow:

> **Monitor → Detect → Triage → Investigate → Remediate → Verify → Document**

---

## 🎯 Project Objective

Build and operate a small simulated NOC environment capable of monitoring infrastructure, identifying technical issues, investigating alerts, performing remediation, verifying recovery, and documenting incidents.

The project is focused on hands-on skills applicable to:

* IT Support
* Service Desk
* Junior NOC
* Network Support
* Infrastructure Support

---

# 🏗️ Lab Architecture

```text
                              Windows 11 Host
                           VMware Workstation Pro
                                    │
                   ┌────────────────┴────────────────┐
                   │                                 │
                   ▼                                 ▼
           Ubuntu Server 24.04                    EVE-NG
              Ubuntu-NOC                         Network Lab
             192.168.80.131                         │
                   │                           ┌─────┴─────┐
          ┌────────┼────────┐                  │           │
          │        │        │                  ▼           ▼
          ▼        ▼        ▼              R1-NOC      SW1-NOC
       Zabbix    MySQL    Apache               │           │
          │                                    └─────┬─────┘
          │                                          │
          ▼                                    NOC Hosts
      SNMP Monitoring                         Host01 / Host02
          │
          ▼
    Metrics / Alerts
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

# 🛠️ Technology Stack

| Category           | Technologies                 |
| ------------------ | ---------------------------- |
| Operating System   | Ubuntu Server 24.04 LTS      |
| Monitoring         | Zabbix 7.4                   |
| Network Monitoring | SNMP / SNMPv2c               |
| Database           | MySQL                        |
| Web Server         | Apache 2                     |
| Network Simulation | EVE-NG Pro 7.2.0-4-PRO       |
| Packet Analysis    | Wireshark                    |
| Virtualization     | VMware Workstation Pro       |
| Administration     | SSH, Bash, APT, systemd      |
| Networking         | TCP/IP, DNS, DHCP, UDP, SNMP |

---

# ✅ Completed Work

## 1. Ubuntu Server Monitoring Environment

* Deployed **Ubuntu Server 24.04 LTS**
* Configured network addressing
* Verified network connectivity
* Verified DNS resolution
* Configured SSH remote administration
* Installed **Zabbix Server 7.4**
* Configured **MySQL** database backend
* Configured **Apache** web frontend
* Installed and configured **Zabbix Agent**
* Verified CPU, memory, and disk monitoring
* Installed and configured **SNMP**
* Verified SNMP service operation
* Verified SNMP UDP/161 listener
* Successfully performed local SNMP polling
* Successfully performed network SNMP polling

---

## 2. EVE-NG Network Environment

* Deployed **EVE-NG Pro 7.2.0-4-PRO**
* Configured virtual networking
* Troubleshot an initial Bridged/Wi-Fi connectivity issue
* Reconfigured EVE-NG using NAT + DHCP
* Verified EVE-NG web access
* Created the NOC network topology
* Configured the management network
* Added router, switch, and host nodes

### Current EVE-NG Topology

```text
                 Cloud0 / Management
                         │
                         │
                   R1-NOC-Router
                         │
                    SW1-NOC-Switch
                      /        \
                     /          \
             NOC-Host01      NOC-Host02
```

---

# 📡 SNMP Configuration & Verification

SNMP has been installed and configured on the Ubuntu monitoring environment.

### SNMP Configuration

```text
SNMP Version: SNMPv2c
Community: public
Monitoring Server: Ubuntu-NOC
IP Address: 192.168.80.131
Port: UDP 161
```

### Network SNMP Polling

Successful SNMP polling was verified using:

```bash
snmpwalk -v2c -c public 192.168.80.131 1.3.6.1.2.1.1
```

The successful response returned standard system information including:

* System description
* System uptime
* System name
* Standard SNMP system OIDs

This confirms that the Ubuntu monitoring server can respond to SNMP requests over the network.

---

# 🔧 Troubleshooting Performed

This project documents real troubleshooting performed during deployment rather than only following installation instructions.

## Zabbix Dependency Issues

**Problem:** Initial Zabbix package dependencies and environment compatibility issues.

**Investigation:** Reviewed package compatibility and the monitoring server environment.

**Resolution:** Rebuilt the monitoring server using Ubuntu Server 24.04 LTS and installed the compatible Zabbix environment.

---

## Zabbix Database Initialization

**Problem:** Database initialization and schema import issues.

**Investigation:** Checked MySQL configuration, privileges, database state, and schema initialization.

**Resolution:** Corrected the database configuration and completed a clean schema import.

---

## EVE-NG Connectivity

**Problem:** EVE-NG was initially unreachable when configured with Bridged networking over Wi-Fi.

**Investigation:** Tested VM networking and host-to-VM connectivity.

**Resolution:** Changed the EVE-NG virtual machine to **NAT + DHCP** and verified access to the EVE-NG web interface.

---

## SNMP Network Polling

**Problem:** Remote SNMP polling initially failed.

**Investigation:** Checked the SNMP service, listening sockets, and configuration.

The SNMP daemon was initially restricted to localhost:

```text
127.0.0.1:161
[::1]:161
```

A conflicting `agentaddress` configuration was identified in:

```text
/etc/snmp/snmpd.conf
```

**Resolution:** Removed the conflicting localhost binding and restarted the SNMP service.

The SNMP service was then verified listening on:

```text
0.0.0.0:161
```

Network SNMP polling subsequently succeeded against:

```text
192.168.80.131
```

### Troubleshooting Method

```text
Problem
   ↓
Investigation
   ↓
Root Cause
   ↓
Remediation
   ↓
Verification
```

---

# 📊 NOC Monitoring Workflow

The target operational workflow for the completed project is:

```text
Infrastructure
      ↓
Monitoring
      ↓
Metrics / Availability
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

The monitoring infrastructure and network lab are currently built. The next phase connects the infrastructure to Zabbix and demonstrates this workflow through simulated incidents.

---

# 🚨 Planned Incident Scenarios

The incident-response phase will simulate realistic NOC events such as:

* Host/device unavailable
* Packet loss
* High CPU utilization
* High memory utilization
* Network interface failure
* DNS resolution failure
* DHCP failure
* SNMP service failure
* Service availability failure
* Network connectivity problems

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

The following screenshots document the actual implementation completed so far.

---

## 01 — Ubuntu Network Configuration

![Ubuntu Network Configuration](screenshots/01-ubuntu-network-interface.png)

Verified the Ubuntu monitoring server's network interface, IP configuration, and connectivity.

---

## 02 — SSH Service

![SSH Service Running](screenshots/02-ubuntu-ssh-service-running.png)

Verified that SSH is running and available for remote Linux administration.

---

## 03 — SNMP Service

![SNMP Service Running](screenshots/03-ubuntu-snmp-service-running.png)

Verified that the SNMP daemon is running on the Ubuntu monitoring server.

---

## 04 — Zabbix Dashboard

![Zabbix Dashboard](screenshots/04_zabbix_dashboard_first_login.png)

Verified successful deployment and access to the Zabbix monitoring platform.

---

## 05 — Live Host Monitoring

![Zabbix Live Host Monitoring](screenshots/05_ubuntu_host_monitored.png)

Verified that Zabbix is collecting live host metrics including CPU, memory, and disk information.

---

## 06 — EVE-NG Web Interface

![EVE-NG Web Interface](screenshots/06_eveng_web_dashboard_login.png)

Verified successful deployment and web access to the EVE-NG network simulation environment.

---

## 07 — EVE-NG NOC Topology

![EVE-NG NOC Topology](screenshots/07-eveng-noc-topology.png)

Shows the completed NOC network topology containing the management network, router, switch, and host nodes.

---

## 08 — Successful Network SNMP Polling

![Successful Network SNMP Poll](screenshots/08-SNMP-Network-Poll-Success.png)

Verified successful SNMPv2c polling of the Ubuntu monitoring server over the network.

This confirms that the SNMP service is reachable remotely and ready for integration with Zabbix monitoring.

---

# 🧠 Skills Demonstrated

## Linux & Systems Administration

* Ubuntu Server 24.04
* Bash
* APT
* systemd
* SSH
* Linux networking
* Service troubleshooting

## Monitoring

* Zabbix Server 7.4
* Zabbix Agent
* Host monitoring
* CPU/memory/disk monitoring
* SNMP
* SNMPv2c
* SNMP polling
* Monitoring architecture

## Networking

* TCP/IP
* DNS
* DHCP
* UDP
* SNMP
* Network connectivity troubleshooting
* Virtual networking
* EVE-NG

## Infrastructure

* VMware Workstation Pro
* EVE-NG
* Linux server deployment
* NAT
* DHCP
* Virtual network environments

## Troubleshooting

* Root-cause analysis
* Fault isolation
* Configuration analysis
* Service troubleshooting
* Network troubleshooting
* Evidence collection
* Verification

## Incident Response

* Alert triage
* Incident investigation
* Root-cause analysis
* Remediation
* Recovery verification
* Incident documentation

---

# 📈 Project Progress

## Monitoring Infrastructure

* [x] Ubuntu Server 24.04 LTS
* [x] Network configuration
* [x] DNS/connectivity verification
* [x] SSH configuration
* [x] Zabbix Server 7.4
* [x] MySQL
* [x] Apache
* [x] Zabbix Agent
* [x] Live host metrics
* [x] SNMP installation
* [x] SNMP configuration
* [x] Local SNMP polling
* [x] Network SNMP polling

## EVE-NG Network Lab

* [x] EVE-NG deployment
* [x] Virtual networking
* [x] Management network
* [x] NOC topology
* [x] Router node
* [x] Switch node
* [x] Host nodes

## Zabbix Network Monitoring

* [ ] Add SNMP-monitored host to Zabbix
* [ ] Configure SNMP interface
* [ ] Apply SNMP monitoring template
* [ ] Verify live SNMP metrics
* [ ] Configure triggers
* [ ] Generate Zabbix Problems/Alerts

## Incident Response

* [ ] Simulate NOC incident
* [ ] Detect incident through monitoring
* [ ] Perform technical investigation
* [ ] Capture Wireshark evidence
* [ ] Identify root cause
* [ ] Remediate incident
* [ ] Verify recovery
* [ ] Document incident report

## Final Documentation

* [ ] Complete incident screenshots
* [ ] Add incident reports
* [ ] Update final architecture
* [ ] Finalize README
* [ ] Mark project complete

---

# 📊 Current Project Status

**🟡 In Progress**

### Estimated Completion: ~70%

### Completed

**Infrastructure Foundation**

Ubuntu Server + Zabbix + MySQL + Apache + SSH

**Network Monitoring Foundation**

SNMP installation + configuration + successful network polling

**Network Simulation**

EVE-NG deployment + networking + completed NOC topology

**Technical Evidence**

8 implementation screenshots documenting the current build

### Current Phase

**Zabbix SNMP Monitoring Integration**

### Remaining Phase

```text
Zabbix SNMP Integration
        ↓
Live SNMP Metrics
        ↓
Triggers / Alerts
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
Incident Documentation
```

---

# 💼 Why This Project Matters

This project demonstrates practical operational skills beyond simply installing monitoring software.

It demonstrates experience with:

* Building a Linux-based monitoring environment
* Configuring and troubleshooting SNMP
* Deploying a virtual network environment
* Monitoring infrastructure
* Troubleshooting connectivity and service issues
* Performing structured root-cause analysis
* Collecting technical evidence
* Following an incident-response workflow
* Documenting technical findings

The project is designed to demonstrate **hands-on skills transferable to entry-level IT Support, Service Desk, Junior NOC, Network Support, and Infrastructure Support roles.**

---

# 👨‍💻 About

**Rikit Thapa**

Computer Systems Networking Technician — Loyalist College
Dean's List

**Career Focus:** IT Support · Service Desk · Junior NOC · Infrastructure Support

### Other Hands-On Projects

* Windows IT Support & Active Directory Lab
* Cisco Campus Network Design
* IT Service Desk & Incident Management Lab
* NOC Infrastructure Monitoring & Incident Response Lab

---

## 📌 Project Status

**🟡 In Progress**

The core monitoring infrastructure, SNMP configuration, EVE-NG environment, and NOC topology have been completed and documented.

The current development phase is integrating **SNMP monitoring with Zabbix**, followed by alert generation, simulated NOC incidents, investigation, Wireshark packet analysis, remediation, recovery verification, and incident documentation.

---

### Project Focus

> **Build → Monitor → Troubleshoot → Investigate → Resolve → Verify → Document**
