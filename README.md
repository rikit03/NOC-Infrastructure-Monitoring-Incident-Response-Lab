# NOC Infrastructure Monitoring & Incident Response Lab

A hands-on **NOC simulation project** demonstrating practical skills in **infrastructure monitoring, Linux administration, SNMP, network troubleshooting, virtual networking, and incident response**.

Built end-to-end using **Ubuntu Server 24.04 LTS, Zabbix 7.4, EVE-NG, VMware Workstation Pro, and Wireshark**.

The project follows a practical operational workflow:

> **Monitor → Detect → Triage → Investigate → Remediate → Verify → Document**

---

## 🎯 Project Objective

Build and operate a small simulated NOC environment capable of:

* Monitoring infrastructure and network services
* Collecting host and SNMP metrics
* Detecting availability and performance issues
* Investigating technical incidents
* Performing structured troubleshooting and remediation
* Verifying service recovery
* Documenting incidents and technical findings

**Target roles:**

**IT Support · Service Desk · Junior NOC · Network Support · Infrastructure Support**

---

# 🏗️ Architecture

```text
                         Windows 11 Host
                      VMware Workstation Pro
                               │
              ┌────────────────┴────────────────┐
              │                                 │
              ▼                                 ▼
       Ubuntu Server 24.04                   EVE-NG
          Ubuntu-NOC                       Network Lab
       192.168.80.131                          │
              │                         ┌──────┴──────┐
      ┌───────┼────────┐                │             │
      ▼       ▼        ▼                ▼             ▼
   Zabbix   MySQL    Apache        R1-NOC-Router  SW1-NOC-Switch
      │                                      │             │
      │                                      └──────┬──────┘
      │                                             │
      ▼                                       NOC-Host01
  SNMP Monitoring                              NOC-Host02
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

| System     | Address          | Purpose                         |
| ---------- | ---------------- | ------------------------------- |
| Ubuntu-NOC | `192.168.80.131` | Zabbix / SNMP monitoring server |
| EVE-NG     | `192.168.80.132` | Network simulation platform     |
| SNMP       | UDP `161`        | Infrastructure monitoring       |

---

# 🛠️ Technology Stack

| Category           | Technologies                 |
| ------------------ | ---------------------------- |
| OS                 | Ubuntu Server 24.04 LTS      |
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

# ✅ Completed Implementation

## Linux Monitoring Server

* Deployed **Ubuntu Server 24.04 LTS**
* Configured network addressing and connectivity
* Verified DNS resolution
* Configured SSH remote administration
* Installed **Zabbix Server 7.4**
* Configured **MySQL** database backend
* Configured **Apache** web frontend
* Installed and configured **Zabbix Agent**
* Verified live CPU, memory, and disk monitoring
* Installed and configured **SNMP**
* Verified SNMP daemon operation
* Verified UDP/161 listening
* Successfully performed local SNMP polling
* Successfully performed network SNMP polling

---

# 📡 Zabbix SNMP Monitoring

A dedicated Zabbix host was created for SNMP-based monitoring:

```text
Host: Ubuntu-Noc-SNMP
IP: 192.168.80.131
SNMP: UDP/161
Version: SNMPv2c
Template: Linux by SNMP
```

Zabbix successfully collected SNMP-based monitoring data including:

* CPU metrics
* Memory metrics
* System information
* Load averages
* Uptime
* ICMP availability
* Network-related metrics
* Storage/filesystem information

### SNMP Verification

Network-level SNMP connectivity was verified using:

```bash
snmpwalk -v2c -c public 192.168.80.131 1.3.6.1.2.1.1
```

The successful response returned standard SNMP system information including:

* System description
* System uptime
* System name
* SNMP system OIDs

This verified that the SNMP service was reachable over the network and could be monitored by Zabbix.

---

# 🌐 EVE-NG Network Environment

Deployed **EVE-NG Pro 7.2.0-4-PRO** as the network simulation environment.

### Completed

* EVE-NG deployment
* Virtual networking configuration
* NAT + DHCP configuration
* Management network configuration
* Web interface access
* NOC topology creation
* Router node
* Switch node
* Two host nodes

### Current Topology

```text
              Cloud0 / Management
                       │
                       ▼
                R1-NOC-Router
                       │
                       ▼
                SW1-NOC-Switch
                  /          \
                 /            \
        NOC-Host01          NOC-Host02
```

The topology provides a simulated network environment for availability, connectivity, and future network-device monitoring scenarios.

> **Note:** The EVE-NG topology is operational as a simulation environment. Direct Zabbix monitoring of the simulated router/switch is a future enhancement and is not being claimed as completed monitoring functionality.

---

# 🔧 Troubleshooting Performed

This project includes **real troubleshooting performed during deployment**, not just installation screenshots.

---

## SNMP Localhost Binding Issue

### Problem

Remote SNMP polling initially failed because the SNMP daemon was restricted to localhost:

```text
127.0.0.1:161
[::1]:161
```

### Investigation

Checked:

* `snmpd` service status
* UDP listening sockets
* `/etc/snmp/snmpd.conf`
* SNMP configuration entries

Identified a conflicting `agentaddress` configuration.

### Resolution

Removed the conflicting localhost binding and restarted the SNMP service.

### Verification

Confirmed the daemon was listening on:

```text
0.0.0.0:161
```

Network SNMP polling then succeeded against:

```text
192.168.80.131
```

---

## EVE-NG Wi-Fi / Bridged Connectivity Issue

### Problem

EVE-NG was initially unreachable when using bridged networking over Wi-Fi.

### Investigation

Tested VM networking and host-to-VM connectivity.

### Resolution

Reconfigured the EVE-NG VM to:

```text
NAT + DHCP
```

Web access was subsequently verified.

---

## Zabbix Database Configuration Issue

### Problem

The Zabbix server process was running, but the frontend reported that the Zabbix server was not running.

### Investigation

Reviewed the Zabbix server log and identified:

```text
[Z3001] connection to database 'zabbix' failed: [1045] Access denied
database is down: reconnecting in 10 seconds
```

Verified:

* MySQL service was operational
* The `zabbix` database existed
* The `zabbix` MySQL account existed
* Database credentials worked through a direct MySQL connection

### Resolution

Corrected the Zabbix server database authentication configuration and restarted the Zabbix server.

### Verification

Confirmed through Zabbix **System information**:

```text
Zabbix server is running: Yes
Zabbix server version: 7.4.14
```

This restored Zabbix server-side data collection and event processing.

---

## Zabbix SNMP Template Conflict

### Problem

The existing agent-monitored Ubuntu host could not directly inherit the `Linux by SNMP` template because of overlapping inventory, graph, and discovery definitions.

### Investigation

Reviewed:

* Inherited items
* Inventory fields
* Graphs
* Low-level discovery rules
* Existing `Linux by Zabbix agent` template configuration

### Resolution

Kept the existing agent-monitored host unchanged and created a dedicated SNMP host:

```text
Ubuntu-Noc-SNMP
```

using:

```text
Linux by SNMP
```

This separated agent-based and SNMP-based monitoring and allowed SNMP monitoring without disrupting the existing host configuration.

---

# 🚨 Incident Response — SNMP Service Failure

A controlled monitoring incident was created to demonstrate the NOC detection and response workflow.

### Incident Scenario

The Ubuntu SNMP service was intentionally stopped:

```bash
sudo systemctl stop snmpd
```

### Technical Verification

SNMP connectivity was tested using:

```bash
sudo -u zabbix snmpwalk -v2c -c public 192.168.80.131 1.3.6.1.2.1.1.1.0
```

The request timed out, confirming that the simulated SNMP outage was real.

### Zabbix Detection

After the Zabbix server database connection was restored, Zabbix successfully generated Problems for:

```text
Ubuntu-Noc-SNMP
```

including:

```text
Linux: No SNMP data collection
```

and the dedicated incident trigger:

```text
NOC Incident: SNMP Service Unavailable
```

Both were reported as:

```text
PROBLEM
Severity: Warning
```

This demonstrated:

```text
SNMP Service Failure
        ↓
SNMP Polling Failure
        ↓
Zabbix Detection
        ↓
Problem Event
        ↓
Incident Investigation
```

### Current Incident Status

The detection portion of the incident has been successfully demonstrated.

The remaining steps are:

* Investigate the service state
* Restore the SNMP service
* Verify SNMP polling recovery
* Verify Zabbix problem recovery
* Document the incident

---

# 📊 Monitoring Workflow

The environment follows this operational workflow:

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

The monitoring and detection foundation is operational, and the first controlled SNMP incident has successfully generated a Zabbix Problem.

---

# 🚨 Planned Incident Scenarios

## Incident 1 — SNMP Service Failure

**Status: Detection demonstrated**

```text
Stop SNMP Service
       ↓
SNMP Polling Failure
       ↓
Zabbix Problem
       ↓
Investigate
       ↓
Restore Service
       ↓
Verify Recovery
       ↓
Document
```

---

## Incident 2 — Host Availability

Simulate a monitored host becoming unavailable.

```text
Host Unavailable
       ↓
Zabbix Detection
       ↓
Connectivity Investigation
       ↓
Root Cause
       ↓
Remediation
       ↓
Recovery Verification
```

---

## Additional Scenarios

Potential future scenarios include:

* Packet loss
* High CPU utilization
* High memory utilization
* Network interface failure
* DNS resolution failure
* DHCP failure
* Service availability failure
* Network connectivity problems

**Wireshark** will be used where packet-level investigation provides useful evidence.

---

# 📸 Project Evidence

The implementation is supported by screenshots documenting the actual lab build and monitoring results.

### 01 — Ubuntu Network Configuration

![Ubuntu Network Configuration](screenshots/01-ubuntu-network-interface.png)

Verified Ubuntu network configuration and connectivity.

### 02 — SSH Service

![SSH Service](screenshots/02-ubuntu-ssh-service-running.png)

Verified SSH availability for remote Linux administration.

### 03 — SNMP Service

![SNMP Service](screenshots/03-ubuntu-snmp-service-running.png)

Verified the SNMP daemon running on Ubuntu.

### 04 — Zabbix Dashboard

![Zabbix Dashboard](screenshots/04_zabbix_dashboard_first_login.png)

Verified successful Zabbix deployment and frontend access.

### 05 — Live Host Monitoring

![Live Host Monitoring](screenshots/05_ubuntu_host_monitored.png)

Verified Zabbix collection of live host metrics.

### 06 — EVE-NG Web Interface

![EVE-NG Web Interface](screenshots/06_eveng_web_dashboard_login.png)

Verified EVE-NG deployment and web access.

### 07 — EVE-NG NOC Topology

![EVE-NG NOC Topology](screenshots/07-eveng-noc-topology.png)

Shows the simulated NOC network topology.

### 08 — Successful Network SNMP Polling

![SNMP Polling](screenshots/08-SNMP-Network-Poll-Success.png)

Demonstrates successful remote SNMPv2c polling.

### 09 — Zabbix SNMP Host Configuration

![Zabbix SNMP Host](screenshots/09-Zabbix-Ubuntu-SNMP-Host-Configuration.png)

Shows the dedicated SNMP-monitored host and `Linux by SNMP` template configuration.

### 10 — Zabbix SNMP Live Metrics

![Zabbix SNMP Metrics](screenshots/10-Zabbix-SNMP-Live-Metrics.png)

Shows Zabbix successfully collecting SNMP monitoring data.

### 11 — Zabbix SNMP Incident Detected

![Zabbix SNMP Incident](screenshots/11-zabbix-snmp-incident-detected.png)
