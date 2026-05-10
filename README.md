# 🐦 Project Karasu: Active Security Home Lab

## 📌 Overview
Project Karasu is a production security home lab running on a headless Ubuntu Server 24.04 LTS node, purpose-built for cybersecurity monitoring, threat intelligence collection, penetration testing practice, and security automation development. The lab generates real threat data 24/7 and serves as the infrastructure backbone for KohoJiro Cybersecurity & Networking Services.

## 🚦 Current Status: [ACTIVE]
All core services are live and operational.

---

## 🖥️ Infrastructure

### Node 01: karasu-hilo (Server)
* **Hardware:** HP 17z-ca300
* **CPU:** AMD Ryzen 7 4700U
* **RAM:** 16GB DDR4
* **Storage:** 1TB SSD
* **OS:** Ubuntu Server 24.04 LTS (headless)
* **Network:** Tailscale mesh VPN (persistent, key expiry disabled)
* **Status:** ✅ Live

### Node 02: Kumano (Primary Workstation)
* **Hardware:** Lenovo ThinkPad T14 Gen 6
* **OS:** Windows 11 + Kali Linux (VirtualBox)
* **Role:** Management, scanning, pentest operations, report delivery
* **Status:** ✅ Active

---

## 🐳 Docker Stack (karasu-net)

| Service | Role | Status |
|---|---|---|
| Traefik v3 | Reverse proxy, TLS termination | ✅ Live |
| Cowrie | SSH honeypot (port 22) | ✅ Live |
| Pi-hole | Network-wide DNS filtering | ✅ Live |
| Seafile | File sync & backup | ✅ Live |
| Grafana | Attack visualization dashboards | ✅ Live |
| Prometheus | Metrics collection (Cowrie exporter) | ✅ Live |
| Glances | Real-time resource monitoring | ✅ Live |
| karasu-dashboard | Live stats server (Cowrie + Pi-hole + Glances) | ✅ Live |

**Host services (non-Docker):**
* **Fail2Ban** — monitors Cowrie JSON logs via polling backend; bans repeat offenders across all ports after 3 events within 1 hour (24-hour ban).

---

## 🔬 Pentest Lab (pentest-net)

Isolated Docker network (`172.20.0.0/24`) — no internet access, no connectivity to production `karasu-net`.

| Service | Role |
|---|---|
| DVWA | Vulnerable web application target |
| Metasploitable 2 | Vulnerable Linux target |
| MySQL | DVWA database backend |

Scanning and exploitation performed from Kali Linux on Node 02 via LAN.

---

## 📊 Live Threat Intelligence

Cowrie SSH honeypot actively captures real internet attack traffic including:
- Credential stuffing and brute force campaigns
- Automated scanner fingerprinting (Go, libssh, Perl-based tools)
- Post-exploitation command sequences
- Malware download attempts

Fail2Ban automatically bans repeat offenders. Pi-hole blocks malicious DNS queries including C2 and botnet infrastructure domains. AbuseIPDB integration enriches attacker data with community reputation scores.

---

## 🛠️ Automation & Tooling

### Threat Intelligence
* **karasu_cowrie.py** — Weekly Cowrie intelligence report engine. Parses multi-day rotated logs, profiles attackers, enriches top IPs via AbuseIPDB, generates branded PDF reports, and SCPs to Kumano. Scheduled via cron every Monday 06:00 HST.
* **karasu_live_watcher.py** — Real-time Discord webhook alerts on successful SSH logins. Tails `cowrie.json` via `watchdog`, queries AbuseIPDB, enforces per-IP cooldown. Runs as `karasu-watcher.service` systemd unit.
* **karasu_abuse_cache.py** — Shared AbuseIPDB lookup cache module with 7-day TTL. Used by both the weekly report engine and live watcher to avoid redundant API calls.
* **karasu_dashboard.py** — Live stats HTTP server aggregating Cowrie, Pi-hole, and Glances data into a single JSON API, served via Docker container.

### System Operations
* **karasu_update.py** — Unattended weekly apt update/upgrade/autoremove with branded PDF report and SCP delivery to Kumano. Scheduled via cron every Sunday 03:00 HST.
* **karasu_weekly.sh** — Shell wrapper for the weekly Cowrie report pipeline.

### Assessment Toolkit (Node 02)
* **karasu_scan.py** — Structured multi-phase Nmap assessment pipeline. Runs 8 scan types, saves individual results, collates into a summary ready for the report engine.
* **karasu_diff.py** — Scan comparison tool. Compares two `karasu_scan.py` result sets and generates a branded PDF showing changes between assessments.
* **Karasu Report Engine** — Standalone HTML pentest report builder (offline, no API required). Parses Nmap output, performs version-based CVE matching, flags risky ports.
* **karasu_redact.py** — Document redaction tool. Auto-detects and redacts sensitive data (IPs, emails, phone numbers, SSNs, names) from PDF and text documents. Produces branded redacted PDF with redaction summary.

### Business Operations (Node 02)
* **Kohojiro_biz.py** — CLI tool for KohoJiro business operations: billable time tracking, Hawaii GET tax logging and quarterly summaries, client management, and PDF invoice generation.

---

## 💼 Professional Use

Project Karasu is the operational backbone of **KohoJiro Cybersecurity & Networking Services** — a freelance cybersecurity practice based in Hilo, Hawaii offering:
- Network security assessments
- Vulnerability assessment reporting
- SOHO network hardening and installation

Engagements conducted under signed client authorization agreements. All assessment tooling developed and tested in the Karasu lab environment.

---

## 📂 Documentation

Build logs, configuration steps, incident notes, and technical decisions documented in [Lab Notes](./Project-Karasu).

---

## 🎯 Next Milestones
- [ ] First client engagement under KohoJiro
- [ ] Grafana geomap dashboard for attacker origin visualization
- [ ] Let's Encrypt TLS upgrade (pending domain acquisition)
- [ ] Project Karasu portfolio writeup for KohoJiro website
