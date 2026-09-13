# NOC Infrastructure Monitoring & Incident Response Lab

A hands-on **NOC simulation** built to demonstrate practical infrastructure monitoring, Linux administration, network monitoring, troubleshooting, and incident-response skills.

The lab is being built end-to-end using **Ubuntu Server, Zabbix, EVE-NG, VMware Workstation, and Wireshark**, with real troubleshooting performed during the deployment.

---

## 🎯 Project Objective

Build a small NOC environment capable of:

**Monitoring infrastructure → Detecting issues → Investigating alerts → Resolving incidents → Verifying recovery → Documenting findings**

The project focuses on practical skills relevant to:

* IT Support
* Service Desk
* Junior NOC
* Infrastructure Support

---

## 🏗️ Current Architecture

```text
                    Windows 11 Host
                 VMware Workstation Pro
                          │
             ┌────────────┴────────────┐
             │                         │
             ▼                         ▼
      Ubuntu Server 24.04          EVE-NG
             │                  Network Lab
             │                         │
       ┌─────┼─────┐             Network Devices
       ▼     ▼     ▼
    Zabbix  MySQL Apache
       │
       ▼
 Zabbix Agent
       │
       ▼
 Live System Metrics
```

> Network-device SNMP monitoring, alerting, incident simulation, and Wireshark investigation will be added in the next phase.

---

## 🛠️ Technology Stack

| Area               | Technologies            |
| ------------------ | ----------------------- |
| OS                 | Ubuntu Server 24.04 LTS |
| Monitoring         | Zabbix 7.4              |
| Database           | MySQL                   |
| Web Server         | Apache 2                |
| Network Monitoring | SNMP                    |
| Network Lab        | EVE-NG                  |
| Packet Analysis    | Wireshark               |
| Virtualization     | VMware Workstation Pro  |
| Administration     | SSH, Bash, APT, systemd |

---

# ✅ Completed So Far

### Ubuntu Server & Zabbix

* Deployed **Ubuntu Server 24.04 LTS**
* Configured and verified network connectivity
* Verified DNS resolution and IP configuration
* Configured **SSH** for remote administration
* Installed **Zabbix Server 7.4**
* Configured **MySQL** database backend
* Configured **Apache** web server
* Installed and configured the **Zabbix Agent**
* Verified live **CPU, memory, and disk metrics** in Zabbix
* Enabled and verified **SNMP** on the monitoring environment

### EVE-NG

* Deployed EVE-NG in a dedicated VMware virtual machine
* Configured virtual networking
* Troubleshot an initial **Bridged/Wi-Fi connectivity issue**
* Reconfigured the VM using **NAT + DHCP**
* Verified access to the EVE-NG web interface

---

# 🔧 Troubleshooting Performed

This project includes real troubleshooting encountered during the build rather than following a completely scripted installation.

| Issue                                   | Root Cause                                                                              | Resolution                                                           |
| --------------------------------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Zabbix dependency errors                | Initial Ubuntu environment was incompatible with the required Zabbix package repository | Rebuilt the monitoring server on Ubuntu 24.04 LTS                    |
| Zabbix database initialization problems | Database privileges, MySQL configuration, and interrupted schema import                 | Corrected database configuration and performed a clean schema import |
| EVE-NG unreachable                      | Bridged networking over Wi-Fi failed to provide reliable connectivity                   | Switched the VM to NAT + DHCP                                        |

### What I Practiced

**Problem → Investigation → Root Cause → Fix → Verification**

This is the same structured approach I will use for the simulated NOC incidents in the next phase.

---

# 📊 Monitoring Workflow

The final monitoring workflow will follow:

```text
Infrastructure
      ↓
Monitoring
      ↓
Metric / Availability Check
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
Verification
      ↓
Documentation
```

---

# 🚨 Planned Incident Scenarios

Once network-device monitoring is connected, the lab will simulate common NOC incidents such as:

* Device / host unavailable
* Packet loss
* High interface utilization
* High CPU utilization
* High memory utilization
* DNS resolution failure
* DHCP failure
* Network interface failure
* Service availability failure

Where appropriate, **Wireshark** will be used to collect packet-level evidence during investigations.

---

# 📸 Current Evidence

### 01 — Ubuntu Network Configuration

Verified IP configuration, interface status, and connectivity.

### 02 — SSH Service

Confirmed remote administration access to the Ubuntu monitoring server.

### 03 — Zabbix Dashboard

Verified the Zabbix monitoring platform and web frontend are operational.

### 04 — Live Host Monitoring

Confirmed Zabbix Agent metrics for CPU, memory, and disk are being collected.

### 05 — EVE-NG Web Interface

Verified EVE-NG is deployed and accessible after resolving the initial networking issue.

> Additional screenshots will be added as each phase is completed.

---

# 🧠 Skills Demonstrated

### Linux & Systems

* Ubuntu Server administration
* Bash
* APT
* systemd
* SSH
* Linux networking

### Monitoring

* Zabbix Server
* Zabbix Agent
* Host monitoring
* Resource monitoring
* SNMP
* Alerts and triggers *(next phase)*

### Networking

* TCP/IP
* DNS
* DHCP
* SNMP
* Connectivity troubleshooting
* Network monitoring *(next phase)*

### Infrastructure

* VMware Workstation
* EVE-NG
* NAT / DHCP
* Virtual networking

### Troubleshooting

* Root-cause analysis
* Fault isolation
* Configuration troubleshooting
* Evidence collection
* Incident documentation

---

# 📈 Project Progress

### Monitoring Infrastructure

* [x] Ubuntu Server 24.04 LTS
* [x] Network configuration verified
* [x] SSH configured
* [x] Zabbix Server installed
* [x] MySQL configured
* [x] Apache configured
* [x] Zabbix Agent configured
* [x] Live host metrics verified
* [x] SNMP enabled

### Network Monitoring & Incident Response

* [x] EVE-NG deployed
* [x] EVE-NG networking verified
* [ ] Build network topology
* [ ] Connect network devices to Zabbix
* [ ] Configure SNMP monitoring
* [ ] Configure triggers and alerts
* [ ] Simulate NOC incidents
* [ ] Investigate incidents with Wireshark
* [ ] Document incident reports
* [ ] Finalize screenshots and documentation

---

# 💼 Why This Project Matters

This project is designed to demonstrate more than the ability to install monitoring software.

It demonstrates the ability to:

* Build and configure a Linux monitoring environment
* Troubleshoot infrastructure problems
* Monitor system resources and availability
* Prepare for network-device monitoring
* Investigate alerts methodically
* Collect technical evidence
* Apply a repeatable incident-response process
* Document technical findings clearly

The goal is to demonstrate **hands-on operational skills that can transfer to an entry-level IT Support or Junior NOC environment.**

---

# 👨‍💻 About

**Rikit Thapa**
Computer Systems Networking Technician — Loyalist College
Dean's List

**Focus:** IT Support · Service Desk · Junior NOC · Infrastructure Support

### Other Hands-On Projects

* **Windows IT Support & Active Directory Lab**
* **Cisco Campus Network Design**
* **IT Service Desk & Incident Management Lab**
* **NOC Infrastructure Monitoring & Incident Response Lab**

---

## 📌 Project Status

**Status:** 🟡 In Progress

**Completed:** Ubuntu + Zabbix monitoring foundation and EVE-NG deployment

**Next:** Network topology → SNMP monitoring → Alerting → Incident simulation → Wireshark investigation → Incident documentation
