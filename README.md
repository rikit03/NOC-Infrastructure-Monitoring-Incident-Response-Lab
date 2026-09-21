# NOC Infrastructure Monitoring & Incident Response Lab

A hands-on **NOC simulation project** demonstrating practical skills in **infrastructure monitoring, Linux administration, SNMP, network troubleshooting, virtual networking, incident detection, remediation, and recovery verification**.

Built end-to-end using **Ubuntu Server 24.04 LTS, Zabbix 7.4, EVE-NG, VMware Workstation Pro, and Wireshark**.

The project follows a practical operational workflow:

> **Monitor → Detect → Triage → Investigate → Remediate → Verify → Document**

---

## 🎯 Project Objective

Build and operate a small simulated NOC environment capable of:

* Monitoring infrastructure and network availability
* Collecting host and SNMP metrics
* Detecting service and connectivity failures
* Investigating technical incidents
* Performing structured troubleshooting and remediation
* Verifying service recovery
* Documenting technical findings

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
              │                                │
      ┌───────┼────────┐                 Cloud0 / Management
      │       │        │                         │
      ▼       ▼        ▼                         ▼
   Zabbix   MySQL    Apache              R1-NOC-Router
      │                                           │
      │                              ┌────────────┴────────────┐
      │                              │                         │
      │                              ▼                         ▼
      │                         NOC-Host01                NOC-Host02
      │                        192.168.100.10            192.168.101.10
      │
      ├── SNMP Monitoring
      │
      └── ICMP Monitoring of R1
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

| System        | Address          | Purpose                                  |
| ------------- | ---------------- | ---------------------------------------- |
| Ubuntu-NOC    | `192.168.80.131` | Zabbix / SNMP monitoring server          |
| EVE-NG        | `192.168.80.132` | Network simulation platform              |
| R1-NOC-Router | `192.168.80.133` | Simulated router / ICMP-monitored device |
| SNMP          | UDP `161`        | Ubuntu infrastructure monitoring         |

### Simulated Network

| Device        | Address             | Purpose                  |
| ------------- | ------------------- | ------------------------ |
| R1-NOC-Router | `192.168.100.1/24`  | NOC network gateway      |
| R1-NOC-Router | `192.168.101.1/24`  | Second simulated network |
| NOC-Host01    | `192.168.100.10/24` | Simulated endpoint       |
| NOC-Host02    | `192.168.101.10/24` | Simulated endpoint       |

R1 was configured with separate interfaces for the two simulated networks, and connectivity between the hosts was verified through the router.

---

# 🛠️ Technology Stack

| Category                | Technologies                 |
| ----------------------- | ---------------------------- |
| Operating System        | Ubuntu Server 24.04 LTS      |
| Monitoring              | Zabbix 7.4                   |
| Network Monitoring      | SNMP / SNMPv2c               |
| Availability Monitoring | ICMP                         |
| Database                | MySQL                        |
| Web Server              | Apache 2                     |
| Network Simulation      | EVE-NG Pro 7.2.0-4-PRO       |
| Packet Analysis         | Wireshark                    |
| Virtualization          | VMware Workstation Pro       |
| Linux Administration    | SSH, Bash, APT, systemd      |
| Networking              | TCP/IP, DNS, DHCP, UDP, SNMP |
| Routing                 | FRRouting (FRR)              |

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
* Performed local SNMP polling
* Performed remote network SNMP polling
* Verified Zabbix server-side data collection and event processing

---

# 📡 Zabbix Monitoring

The project uses two different monitoring approaches.

### Ubuntu-Noc-Server

Monitored using:

```text
Zabbix Agent
```

Used for standard Linux host monitoring including CPU, memory, disk, and system metrics.

### Ubuntu-Noc-SNMP

Dedicated SNMP-monitored host:

```text
Host: Ubuntu-Noc-SNMP
IP: 192.168.80.131
Protocol: SNMPv2c
Port: UDP/161
Template: Linux by SNMP
```

Zabbix successfully collected SNMP-based data including:

* CPU metrics
* Memory metrics
* System information
* Load averages
* Uptime
* Network-related metrics
* Storage/filesystem information
* Availability information

### SNMP Verification

Network-level SNMP connectivity was verified using:

```bash
snmpwalk -v2c -c public 192.168.80.131 1.3.6.1.2.1.1
```

The successful response returned standard SNMP system information, confirming that SNMP was reachable over the network.

---

# 🌐 EVE-NG Network Environment

**EVE-NG Pro 7.2.0-4-PRO** was deployed as the network simulation platform.

### Completed

* EVE-NG deployment
* NAT + DHCP configuration
* Management network configuration
* Web interface access
* NOC topology creation
* FRRouting router deployment
* Virtual host deployment
* Router interface configuration
* Inter-network connectivity testing
* R1 management connectivity
* ICMP monitoring of the simulated router

### Current Topology

```text
                  Cloud0 / Management
                          │
                          ▼
                   R1-NOC-Router
                  /             \
                 /               \
                ▼                 ▼
          NOC-Host01          NOC-Host02
        192.168.100.10       192.168.101.10
```

The EVE-NG environment provides a simulated network in which availability, routing, connectivity, and monitoring scenarios can be tested.

A switch node is retained in the EVE-NG project as part of the lab environment, but the currently monitored traffic path uses the working direct R1-to-host topology.

---

# 📊 R1 Availability Monitoring

The simulated FRR router was added to Zabbix as:

```text
Host: R1-NOC-Router
Management IP: 192.168.80.133
Monitoring: ICMP
```

Zabbix successfully collected:

* ICMP availability
* ICMP packet loss
* ICMP response time

Example healthy state:

```text
ICMP Ping: Up (1)
ICMP Loss: 0%
ICMP Response Time: ~1 ms
```

This demonstrates practical monitoring of a network device's **availability and response time** without claiming unsupported SNMP functionality.

---

# 🔧 Troubleshooting Performed

This project includes **real troubleshooting performed during deployment and testing**, rather than only following installation procedures.

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

A conflicting `agentaddress` configuration was identified.

### Resolution

Removed the conflicting localhost binding and restarted the SNMP service.

### Verification

Confirmed the daemon was listening on:

```text
0.0.0.0:161
```

Remote SNMP polling then succeeded against:

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

Reconfigured the EVE-NG VM to use:

```text
NAT + DHCP
```

Web access was subsequently verified.

---

## Zabbix Database Authentication Issue

### Problem

The Zabbix frontend reported that the Zabbix server was not running even though the service process was active.

### Investigation

Reviewed the Zabbix server logs and identified a database authentication failure:

```text
[Z3001] connection to database 'zabbix' failed: [1045] Access denied
database is down: reconnecting in 10 seconds
```

Verified:

* MySQL service was operational
* Zabbix database existed
* Zabbix MySQL account existed
* Database credentials worked through direct MySQL testing

### Resolution

Corrected the Zabbix server database authentication configuration and restarted the Zabbix server.

### Verification

Confirmed through Zabbix System Information:

```text
Zabbix server is running: Yes
Zabbix server version: 7.4.14
```

This restored server-side monitoring and event processing.

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
* Existing `Linux by Zabbix agent` configuration

### Resolution

Kept the existing agent-monitored host unchanged and created a dedicated:

```text
Ubuntu-Noc-SNMP
```

host using:

```text
Linux by SNMP
```

This separated agent-based and SNMP-based monitoring while avoiding conflicts.

---

# 🚨 Incident Response

Two controlled incidents were successfully simulated and recovered.

The incident workflow used throughout the project was:

```text
Detect
  ↓
Triage
  ↓
Investigate
  ↓
Remediate
  ↓
Verify Recovery
  ↓
Document
```

---

## Incident 1 — SNMP Service Failure

### Scenario

The Ubuntu SNMP service was intentionally stopped:

```bash
sudo systemctl stop snmpd
```

### Investigation

SNMP connectivity was tested using:

```bash
sudo -u zabbix snmpwalk -v2c -c public 192.168.80.131 1.3.6.1.2.1.1.1.0
```

The request timed out, confirming the simulated monitoring failure.

### Zabbix Detection

Zabbix generated Problems for:

```text
Ubuntu-Noc-SNMP
```

including:

```text
Linux: No SNMP data collection
NOC Incident: SNMP Service Unavailable
```

Both were reported as:

```text
PROBLEM
Severity: Warning
```

### Response

The SNMP service was restored and SNMP polling was verified again.

### Result

The incident demonstrated the complete monitoring cycle:

```text
SNMP Service Failure
        ↓
SNMP Polling Failure
        ↓
Zabbix Detection
        ↓
Problem Event
        ↓
Investigation
        ↓
Service Recovery
        ↓
Monitoring Verification
```

---

## Incident 2 — Router Availability Failure

### Scenario

The monitored FRR router:

```text
R1-NOC-Router
192.168.80.133
```

was intentionally stopped in EVE-NG.

### Zabbix Detection

Zabbix detected the loss of ICMP connectivity and generated:

```text
ICMP Ping: Unavailable by ICMP ping
```

with:

```text
Severity: High
```

### Recovery

The router was restarted in EVE-NG.

Connectivity was then verified from Ubuntu:

```bash
ping -c 4 192.168.80.133
```

Successful replies confirmed network recovery.

Zabbix subsequently recorded the event as:

```text
RESOLVED
```

with a recorded recovery time.

### Result

This demonstrated:

```text
Router Failure
      ↓
ICMP Monitoring Failure
      ↓
Zabbix High-Severity Problem
      ↓
Infrastructure Recovery
      ↓
Connectivity Verification
      ↓
Zabbix Recovery
```

---

# 📈 Monitoring & Incident Workflow

The completed environment follows:

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

The lab demonstrates both **service-level monitoring through SNMP** and **network-device availability monitoring through ICMP**.

---

# 📸 Project Evidence

The implementation is supported by screenshots documenting the actual build, monitoring, troubleshooting, and incident-response work.

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

Verified Zabbix collection of live Linux host metrics.

### 06 — EVE-NG Web Interface

![EVE-NG Web Interface](screenshots/06_eveng_web_dashboard_login.png)

Verified EVE-NG deployment and web access.

### 07 — EVE-NG NOC Topology

![EVE-NG NOC Topology](screenshots/07-eveng-noc-topology.png)

Shows the simulated NOC network environment.

### 08 — Successful Network SNMP Polling

![SNMP Polling](screenshots/08-SNMP-Network-Poll-Success.png)

Demonstrates successful remote SNMPv2c polling.

### 09 — Zabbix SNMP Host Configuration

![Zabbix SNMP Host](screenshots/09-Zabbix-Ubuntu-SNMP-Host-Configuration.png)

Shows the dedicated SNMP-monitored host and `Linux by SNMP` configuration.

### 10 — Zabbix SNMP Live Metrics

![Zabbix SNMP Metrics](screenshots/10-Zabbix-SNMP-Live-Metrics.png)

Shows Zabbix successfully collecting SNMP monitoring data.

### 11 — SNMP Incident Detected

![Zabbix SNMP Incident](screenshots/11-zabbix-snmp-incident-detected.png)

Shows Zabbix detecting the simulated SNMP service failure.

### 12 — R1 Router Incident Detected

![R1 Incident Detected](screenshots/12-zabbix-r1-incident-detected.png)

Shows Zabbix detecting the simulated R1 router availability failure with a High-severity ICMP problem.

### 13 — R1 Incident Recovered

![R1 Incident Recovered](screenshots/13-zabbix-r1-incident-recovered.png)

Shows the R1 incident transitioning to **RESOLVED** after router recovery and connectivity verification.

---

# 🧠 Skills Demonstrated

### Monitoring & NOC Operations

* Zabbix server deployment
* Host monitoring
* SNMP monitoring
* ICMP availability monitoring
* Alert/problem investigation
* Incident detection
* Recovery verification
* Monitoring validation

### Linux Administration

* Ubuntu Server administration
* SSH
* Bash
* APT package management
* systemd service management
* SNMP configuration
* Network troubleshooting
* Service verification

### Networking

* TCP/IP
* IPv4 addressing
* DNS
* DHCP
* UDP
* SNMP
* ICMP
* Routing
* Virtual networking
* Network connectivity troubleshooting

### Network Simulation

* EVE-NG
* FRRouting
* Virtual network topology design
* Router interface configuration
* Simulated endpoint connectivity

### Troubleshooting

* Log analysis
* Service-state investigation
* Configuration troubleshooting
* Database authentication troubleshooting
* SNMP connectivity troubleshooting
* Network connectivity testing
* Incident isolation
* Recovery validation

### Tools

* Zabbix
* EVE-NG
* VMware Workstation Pro
* Wireshark
* MySQL
* Apache
* SSH
* Bash
* Linux networking utilities

---

# 📋 Project Status

| Component                         | Status     |
| --------------------------------- | ---------- |
| Ubuntu Monitoring Server          | ✅ Complete |
| Zabbix Server                     | ✅ Complete |
| Zabbix Agent Monitoring           | ✅ Complete |
| SNMP Monitoring                   | ✅ Complete |
| EVE-NG Environment                | ✅ Complete |
| Network Simulation                | ✅ Complete |
| R1 ICMP Monitoring                | ✅ Complete |
| Incident Detection                | ✅ Complete |
| SNMP Incident Recovery            | ✅ Complete |
| R1 Availability Incident Recovery | ✅ Complete |
| Troubleshooting Documentation     | ✅ Complete |
| Project Evidence                  | ✅ Complete |
| README Documentation              | ✅ Complete |

### Overall Status

**🟢 Complete**

---

# 💼 Project Value

This project demonstrates the practical workflow used in entry-level **IT Support, Service Desk, NOC, Network Support, and Infrastructure Support** environments:

> **Monitor → Detect → Investigate → Troubleshoot → Remediate → Verify → Document**

Rather than only configuring monitoring software, the project demonstrates the complete operational cycle by creating controlled infrastructure failures, analyzing monitoring results, restoring affected services, and verifying recovery.

---

# 🚀 Future Enhancements

Possible future extensions include:

* High CPU incident simulation
* High memory utilization incident
* Packet-loss investigation
* Network interface failure simulation
* DNS failure scenario
* DHCP troubleshooting scenario
* Additional Linux hosts
* Microsoft 365 / Entra ID integration
* PowerShell-based monitoring automation

These are optional extensions and are **not required for the completed project**.

---

# 👨‍💻 About

Built as a hands-on portfolio project to demonstrate practical **IT infrastructure monitoring, Linux administration, networking, troubleshooting, and NOC incident-response skills**.

**Focus:** IT Support · Service Desk · Junior NOC · Network Support · Infrastructure Support

---

## Project Status

**🟢 Complete — Core monitoring, network simulation, incident detection, recovery, troubleshooting, and documentation demonstrated.**
