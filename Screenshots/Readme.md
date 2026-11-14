
<div align="center">

# 🛡️ PENETRATION TESTING

### 🚀 Week 2 Project | Networkwalks Internship (`Batch B084A`)

<div align="center">

# 🛡️ PENETRATION TESTING

### 🚀 Week 2 Project | Networkwalks Internship (`Batch B084A`)

<p>
  <img src="https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white">
  <img src="https://img.shields.io/badge/Maltego-183A61?style=for-the-badge&logo=virtualbox&logoColor=white">
  <img src="https://img.shields.io/badge/Networking-0078D4?style=for-the-badge">
  <img src="https://img.shields.io/badge/Cybersecurity-Learning-success?style=for-the-badge">
</p>

*Footprinting Public Infrastructure | Visual OSINT Mapping | Active LAN Discovery*

</div>

---

## 📋 Project Overview

| Field | Details |
| :--- | :--- |
| **Pentester Name** | **Fiza Nadeem** *(Cybersecurity Professional)* |
| **Program / Batch** | `B084A-Networkwalks` |
| **Mentor** | **Sir Waqas Karim** |
| **Assessment Date** | 14 November 2026 |
| **Modules Completed** | `W2-PM1` (Kali CLI Tools) • `W2-PM3` (Maltego OSINT) • `W2-PM5` (Zenmap Scanning) |
| **Authorized Targets** | 1. **Networkwalks** (`networkwalks.com` — *written permission secured*)<br>2. **Personal Local LAN Network** |
| **Client Permission** | ✅ Yes |
| **Phases Covered** | **Phase 1:** Reconnaissance & Footprinting *(Completed)*<br>**Phase 2:** Scanning & Network Discovery *(Completed)*<br>**Phases 3–5:** Exploitation, Post-Exploitation & Reporting *(In Progress)* |

> [!IMPORTANT]
> ### ⚠️ Liability Disclaimer
> All activities documented in this report were performed strictly on systems and devices where explicit written permission was obtained or on personally owned lab networks. These materials are shared purely for educational and defensive security research. Unauthorized scanning or testing against systems without permission is illegal.

---

## 🎯 Project Introduction

Welcome to my **Week 2 Penetration Testing Project** as part of the **Networkwalks** Cybersecurity & Ethical Hacking Internship!

In this project, I explored the **Footprinting and Network Scanning** phases of penetration testing to understand how much public and local network information can be discovered before any exploitation takes place:
* **Command-Line Footprinting (`W2-PM1`):** Used six Kali Linux terminal tools (`WHOIS`, `WhatWeb`, `nslookup`, `curl -I`, `wafw00f`, and `dnsrecon`) to gather domain records, DNS entries, server headers, web technologies, and firewall details for `networkwalks.com`.
* **Visual OSINT Mapping (`W2-PM3`):** Used **Maltego** to turn raw domain data into an interactive relationship graph linking mail servers, IP blocks, subdomains, and public contacts.
* **Local Network Scanning (`W2-PM5`):** Used **Zenmap** on a Windows host to safely discover live devices, MAC addresses, and network topology across my local subnet.

---

## 🛠️ Tools Used

| Tool / Platform | Role in Assessment |
| :--- | :--- |
| **Kali Linux & Windows** | Operating systems used to run terminal reconnaissance, Maltego graphs, and local network scans. |
| **WHOIS** | Checks public domain registration info, including the registrar, creation/expiry dates, and name servers. |
| **WhatWeb** | Fingerprints the target website to detect its CMS platform, plugins, web server, and front-end libraries. |
| **nslookup** | Queries DNS servers to translate `networkwalks.com` into its hosting IPv4 address. |
| **curl -I** | Fetches HTTP response headers to inspect server configuration and exposed API paths. |
| **wafw00f** | Detects whether a Web Application Firewall (WAF) is protecting the site and identifies the vendor. |
| **dnsrecon** | Enumerates DNS records including Name Servers (`NS`), Mail Servers (`MX`), `SPF`, and `TXT` entries. |
| **Maltego (`W2-PM3`)** | Automates visual OSINT transforms to map connections between domains, IP blocks, and public emails. |
| **Zenmap (Nmap GUI)** | Scans the local subnet to discover active hosts, IP/MAC addresses, and visual network topology. |
| **Windows CMD (`ipconfig`)** | Displays local network adapter details, host IPv4 address, and subnet mask prior to scanning. |

---

## 🔍 Activities & Key Findings

### 1️⃣ Footprinting & Reconnaissance with Kali CLI (`W2-PM1`)
* **WHOIS Lookup:** Confirmed `networkwalks.com` is registered through **GoDaddy.com, LLC** using HostGator name servers (`://hostgator.com` & `://hostgator.com`).
* **WhatWeb Fingerprinting:** Identified **Apache** web server running **WordPress 7.1.4** with the **WP Download Manager 3.3.76** plugin and Bootstrap/jQuery libraries.
* **DNS Resolution (`nslookup`):** Resolved the domain to its public hosting IPv4 address (`192.232.216.135` / `192.232.216.136`).
* **HTTP Header Inspection (`curl -I`):** Returned `HTTP/1.1 200 OK` from Apache, exposing WordPress caching headers (`X-nginx-cache: WordPress`) and the REST API endpoint (`/wp-json/`).
* **Firewall Detection (`wafw00f`):** Confirmed the website is actively protected behind **ModSecurity (SpiderLabs) WAF**.
* **DNS Enumeration (`dnsrecon`):** Collected authoritative `NS`, `MX`, `TXT`, and `SPF` records governing domain routing and email security.

### 2️⃣ Maltego-Based Visual OSINT (`W2-PM3`)
* Created a new investigation graph targeting the `networkwalks.com` domain entity.
* Executed infrastructure transforms to visually map linked **Name Servers**, **Mail Exchangers**, **IPv4 addresses**, and **Netblocks**.
* Mapped **72 connected entities**—including publicly indexed email addresses (`info@networkwalks.com`) and associated web pages—revealing the external attack surface at a glance.

### 3️⃣ Local Network Scanning with Zenmap (`W2-PM5`)
* Checked local adapter configuration via `ipconfig` to confirm the local subnet range.
* Executed a non-intrusive **Ping Scan** across the local subnet to detect active devices without triggering disruptive port exploitation.
* Exported the visual **Network Topology Map** showing how client hosts connect through the local gateway router.

---

## 📊 Risk Analysis & Security Impact

> [!NOTE]
> The items below represent **reconnaissance observations** rather than confirmed exploitable vulnerabilities. No active exploitation was performed.

| # | Risk / Observation | Evidence Found | Potential Security Impact | Risk Level |
| :---: | :--- | :--- | :--- | :---: |
| **1** | **CMS & Plugin Versions Exposed** | `WhatWeb` detected **WordPress 7.1.4** and **WP Download Manager 3.3.76**. | Attackers can search public vulnerability databases for version-specific flaws. | 🟡 **Medium** |
| **2** | **Hosting Server IP Identifiable** | `nslookup` and `Maltego` resolved the public hosting IPv4 address. | Reveals the hosting provider and network location of the origin web server. | 🟢 **Low** |
| **3** | **HTTP Headers & API Path Visible** | `curl -I` exposed server headers and the `/wp-json/` REST API route. | Helps attackers fingerprint server behavior and enumerate API endpoints. | 🟢 **Low** |
| **4** | **WAF Technology Identifiable** | `wafw00f` identified **ModSecurity (SpiderLabs)** guarding the site. | Tells an attacker which firewall rule sets are in place so they can tailor probes. | 🟢 **Low** |
| **5** | **DNS & Infrastructure Mapped** | `dnsrecon` and `Maltego` linked `NS`, `MX`, IPv4, and netblock records. | Exposes shared hosting infrastructure and email routing targets. | 🟡 **Medium** |
| **6** | **Public OSINT & Contact Clues** | `Maltego` uncovered public email addresses (`info@networkwalks.com`). | Exposed staff or organization emails can be targeted for phishing attacks. | 🟡 **Medium** |
| **7** | **Multiple Live LAN Hosts Visible** | `Zenmap` discovered active client devices on the local subnet. | Unmonitored local networks allow unauthorized or rogue devices to go unnoticed. | 🟡 **Medium** |

---

## 🛡️ Security Recommendations

1. **Hide Software Version Details:** Configure WordPress and Apache headers to remove exact CMS and plugin version numbers from public HTML and HTTP responses.
2. **Keep CMS & Plugins Updated:** Apply security patches promptly for WordPress core, themes, and plugins like *WP Download Manager*.
3. **Restrict Unnecessary API Endpoints:** Limit public access to `/wp-json/` REST API routes where unauthenticated access is not required.
4. **Audit Public OSINT Exposure:** Periodically review public DNS records and run self-audits with Maltego to ensure internal subdomains or staff emails are not unnecessarily exposed.
5. **Maintain WHOIS Privacy:** Keep domain registrant contact details masked through registrar privacy protection.
6. **Keep WAF Rules Tuned:** Keep **ModSecurity** in active blocking mode and monitor firewall logs for automated scanning activity.
7. **Monitor Local Networks:** Schedule routine internal discovery scans to verify all connected IP and MAC addresses and investigate unknown devices immediately.

---

## ✅ Conclusion

