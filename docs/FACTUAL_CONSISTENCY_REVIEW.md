---
layout: simple
title: Factual Consistency Review
---

# Factual Consistency Review

Review date: 2026-04-24

This note records the factual consistency fixes made after reviewing the published Teamcenter 2412 installation runbook against the current repository and the validated `server2019tc` host.

## Findings Fixed

| Finding | Resolution |
|---------|------------|
| Fragment page link to `03-windows-features` resolved under `/02-software-prerequisites_frags/` and returned `404`. | Updated the link to `../03-windows-features/` in both the published fragment and Docs Assembler source. |
| Post-install validation used `2412.8` as the generic patched version while the landing page listed installed version `2412.0.0.8`. | Clarified the distinction: installed full version is `2412.0.0.8`; patch/about version is `2412.8`. |
| Root `_config.yml` duplicated published configuration and could drift from `docs/_config.yml`. | Removed the unused root config and documented that GitHub Pages builds from `docs/_config.yml`. |

## Current Evidence

The reviewed host evidence supported the published baseline:

- `C:\TC2412`, `C:\tcdata`, Java, Teamcenter configuration, Server Manager configuration, gateway configuration, `pom_transmit`, and disabled `oci.dll` marker exist.
- SQL Server `MSSQLSERVER`, IIS `W3SVC`, WAS, and `Teamcenter Server Manager TCFISHER_PoolA` are running.
- Ports `80`, `1433`, `3000`, `4544`, `8086`, `8087`, and `8088` are listening.
- `http://server2019tc/tc/services/ServiceDispatcher?wsdl`, `http://server2019tc:3000/`, and `http://server2019tc:3000/tc.html` return `200`.
- TEM recovery check prints `Configuration TCFISHER is not in recovery mode`.

## Version Convention

Use these labels consistently:

| Label | Value |
|-------|-------|
| Base release | `2412` |
| Installed full version | `2412.0.0.8` |
| Patch/about version | `2412.8` |
| Patch package label | `2412.008` |

## April 29 CAD Integration Update

The published runbook was updated from the April 28, 2026 `C:\TC_AI` CAD integration records.

New facts reflected:

- SolidWorks Integration for Teamcenter `2412.1000.0000` server-side deployment was completed and verified.
- Creo Integration for Teamcenter `2412.1000.0000` server-side deployment was completed and verified.
- Teamcenter Integration for CATIA V5 `2412.1004.0000` server-side deployment was completed and verified.
- The active `configuration.xml` was repaired to preserve cleaned TEM recovery state while restoring the context needed for future feature maintenance.
- `configuration2604281149.xml` is the post-success configuration archive for the April 28 CAD integration work.
- FSC on port `4544` is required for CAD model dataset transfer and client file movement.
- SolidWorks and Creo hosted-AW preferences should use `http://server2019tc:3000`, while `http://server2019tc:3000/awc` returning `404` is expected on this host.
- Remaining CAD validation is client-workstation work, not server-host work.
