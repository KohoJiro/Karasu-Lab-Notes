# 🐦 Project Karasu: Active Security Home Lab

## 📌 Overview
Project Karasu is a production security home lab running on 
a headless Ubuntu Server 24.04 LTS node, purpose-built for 
cybersecurity monitoring, threat intelligence collection, 
and penetration testing practice. The lab generates real 
threat data 24/7 and serves as the infrastructure backbone 
for KohoJiro Cybersecurity Services.

## 🚦 Current Status: [ACTIVE]

All core services are live and operational.

## 🖥️ Infrastructure

### Node 01: karasu-hilo (Server)
* **Hardware:** HP 17z-ca300
* **CPU:** AMD Ryzen 7 4700U
* **RAM:** 16GB DDR4
* **Storage:** 1TB SSD
* **OS:** Ubuntu Server 24.04 LTS (headless)
* **Status:** ✅ Live

### Node 02: Primary Workstation
* **Hardware:** Lenovo ThinkPad T14
* **OS:** Windows + Kali Linux (VirtualBox)
* **Role:** Management, scanning, pentest operations
* **Status:** ✅ Active

## 🐳 Docker Stack (karasu-net)

| Service | Role | Status |
|---|---|---|
| Traefik v3 | Reverse proxy, TLS | ✅ Live |
| Cowrie | SSH honeypot (port 22) | ✅ Live |
| Fail2Ban | Intrusion detection & banning | ✅ Live |
| Pi-hole | DNS filtering | ✅ Live |
| Seafile | File sync | ✅ Live |
| Grafana + Prometheus | Monitoring & dashboards | ✅ Live |
| Glances | Resource monitoring | ✅ Live |

## 🔬 Pentest Lab (pentest-net)

Isolated Docker network (172.20.0.0/24) — no internet access.

| Service | Role |
|---|---|
| DVWA | Vulnerable web app target |
| Metasploitable 2 | Vulnerable Linux target |
| MySQL | DVWA backend |

Scanning performed from Kali Linux on Node 02 via LAN.

## 📊 Live Threat Data

Cowrie SSH honeypot actively captures real internet 
attack traffic including:
- Credential stuffing attempts
- Brute force campaigns
- Post-exploitation command sequences
- Malware download attempts

Fail2Ban automatically bans repeat offenders across 
multiple jails (sshd, traefik-auth).

Pi-hole blocks malicious DNS queries including C2 
and botnet infrastructure domains.

## 🛠️ Assessment Toolkit

* **karasu_scan.py** — Automated Nmap assessment pipeline
  (8 structured scans, collated output, report-ready)
* **Karasu Report Engine** — Standalone security report 
  generator (no API required, runs offline)
* **VA-AUTH-001** — Client authorization agreement template

## 💼 Professional Use

Project Karasu serves as the operational foundation for 
[KohoJiro Cybersecurity Services](https://www.fiverr.com/justingerbert/write-a-professional-cybersecurity-assessment-report-from-your-scan-data) — 
offering professional vulnerability assessment report 
writing for small businesses.

## 📂 Documentation

Daily progress logs, configuration steps, and technical 
notes documented in [Lab Notes](./Project-Karasu)

## 🎯 Next Milestones

- [ ] First pentest scan against DVWA
- [ ] First client engagement
- [ ] CompTIA Security+ certification
