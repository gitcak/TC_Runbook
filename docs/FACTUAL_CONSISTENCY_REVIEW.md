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
