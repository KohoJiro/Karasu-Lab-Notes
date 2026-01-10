# 🐦 Project Karasu: Hardened Linux Lab

## 📌 Overview
Project Karasu is a security-focused lab environment designed to explore headless Linux administration, network hardening, and secure remote management. 

## 🚦 Current Status: [STAGED]
This project is currently in the **Procurement & Staging Phase**. 
* **Completed:** Data archival (17.3GB), migration strategy, and bootable media preparation (Ventoy/Rufus).
* **Blocker:** Awaiting final funding for the Primary Management Workstation (Lenovo T14).

## 🖥️ Target Infrastructure

### Node 01: The Server (Karasu)
* **Hardware:** HP 17z-ca300
* **CPU:** AMD Ryzen 7 4700U with Radeon Graphics (2.00 GHz)
* **RAM:** 16GB DDR4
* **Role:** Headless Ubuntu Server 24.04 LTS
* **Status:** **Active Lifecycle Reassignment.** ### 🛡️ Strategy Rationale (The Pivot)
* **Legacy Issue:** HP 17z-ca300 display assembly failure (persistent purple hue) has been a known blocker for standard operations for several months.
* **Resolution Path:** Following architectural review, the decision was made to decommission the unit as a primary workstation and repurpose the healthy internal compute resources (Ryzen 7 / 16GB RAM) as a **Headless Linux Server**.
* **Transition Strategy:**
    1. **Data Preservation:** (Completed Day 0) - Safeguard data before hardware wipe.
    2. **Procurement:** (Current Blocker) - Acquire T14 to serve as the new GUI/Management interface.
    3. **Deployment:** (Next Phase) - Install Ubuntu Server 24.04 LTS on Node 01. 

### Node 02: The Workstation (Planned)
* **Hardware:** Lenovo ThinkPad T14 Gen 6 21QJ00CQUS
* **Requirement Rationale:** Required to replace the primary workstation. The T14 provides the reliable display and virtualization support needed for security auditing that Node 01 can no longer provide.
* **Status:** PENDING PROCUREMENT

## 📂 Documentation
Daily progress logs, technical hurdles, and configuration steps are documented in the [Lab Notes](./Project-Karasu)
