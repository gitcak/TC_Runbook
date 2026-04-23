---
layout: simple
title: Teamcenter 2412 Installation Runbook
---

# Teamcenter 2412 Installation Runbook

**Host:** `server2019tc` &nbsp;|&nbsp; **Version:** `2412.0.0.8` &nbsp;|&nbsp; **Validated:** April 2026

This runbook documents the complete TEM-based installation of Teamcenter 2412 with patch 2412.008 on a single Windows Server 2019 host. It is written for the validated single-host pattern used on this machine.

---

## Sections

| # | Section | Purpose |
|---|---------|---------|
| 1 | [Overview](01-overview) | Purpose, topology, and how to use this guide |
| 2 | [Software Prerequisites](02-software-prerequisites) | Required software, media, Java, SQL Server, IIS |
| 3 | [Windows Features](03-windows-features) | IIS and .NET feature set required |
| 4 | [Operator Worksheet](04-operator-worksheet) | Build profile and values to collect before TEM |
| 5 | [Pre-Install Checklist](05-pre-install-checklist) | Final checks before opening TEM |
| 6 | [TEM Installation](06-tem-installation) | Step-by-step TEM wizard walkthrough |
| 7 | [TEM Panel Reference](07-tem-panel-reference) | Field-level reference for every TEM panel |
| 8 | [Patching](08-patching) | Applying patch 2412.008 after base install |
| 9 | [Post-Install Validation](09-post-install-validation) | Service, port, IIS and URL checks |
| 10 | [Handoff](10-handoff) | Handoff checklist and known conventions |
| 11 | [Troubleshooting](11-troubleshooting) | TEM state recovery, server manager, AWC gateway |

---

## Quick Start

If you already know the topology:

1. Install Windows IIS/.NET features
2. Install and validate SQL Server
3. Install Java 17 and verify the JRE path
4. Expand Teamcenter base and patch media locally
5. Create `TC_ROOT` (`C:\TC2412`) and `TC_DATA` (`C:\tcdata`)
6. Launch TEM: `tem.bat -jre "C:\java\jre"`
7. Install Foundation, Server Manager, Web Tier for .NET, FOSS Repository
8. Apply patch 2412.008
9. Validate IIS, WSDL, server-manager ports, and optional AWC
10. Archive logs under `C:\TC_AI`

---

## Validated Baseline

| Resource | Value |
|----------|-------|
| Teamcenter root | `C:\TC2412` |
| Teamcenter data | `C:\tcdata` |
| Installed version | `2412.0.0.8` |
| SQL Server | `MSSQLSERVER` on port `1433` |
| IIS site | `Default Web Site` |
| Web application | `/tc` |
| App pool | `TcWebTierPool` |
| Server Manager service | `Teamcenter Server Manager TCFISHER_PoolA` |
| Server Manager ports | `8086`, `8087`, `8088` |
| AWC gateway | `http://server2019tc:3000` |
