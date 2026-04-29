# Agent Guide

This repository is the standalone Docs Assembler and GitHub Pages source for the Teamcenter 2412 installation runbook.

## Working Agreement

- Keep work scoped to `C:\TC_Runbook` unless the user explicitly asks for host-level Teamcenter checks.
- This repo is meant to work cleanly with both Codex and Claude Code. Treat this file as the shared agent contract. If a `CLAUDE.md` file is added later, keep its repo facts and workflow rules consistent with this file.
- Prefer evidence from current files, GitHub Pages workflow state, and the local Teamcenter host over memory or assumptions.
- Do not commit secrets, passwords, Siemens Support credentials, local browser sessions, or transient Teamcenter logs.

## Repository Map

- `tsmaps/` contains the Docs Assembler source maps, step fragments, shared variables, and source-bank references.
- `docs/` is the GitHub Pages publish source. The workflow builds Jekyll from this folder.
- `docs/_config.yml` is the active Pages/Jekyll configuration.
- `.github/workflows/pages.yml` deploys `./docs` to GitHub Pages.
- `docs-assembler-config.json` points to owner `gitcak`, repo `TC_Runbook`, branch `main`, and publish URL `https://gitcak.github.io/TC_Runbook/`.
- `.bin/` is local Docs Assembler working state and must stay ignored.
- `pub/` is generated Docs Assembler output and must stay ignored unless the user explicitly changes the publishing model.

## Editing Rules

- For runbook content that is generated from Docs Assembler maps, update both:
  - the source under `tsmaps/.../δ steps/*.tsstp`
  - the corresponding published file under `docs/...`
- For page-level published content such as `docs/index.md`, `docs/404.html`, `docs/_config.yml`, and maintenance notes, edit `docs/` directly.
- Keep generated guide files and fragments internally consistent. If a section page changes, check its matching `_frags` content when applicable.
- Preserve existing file encoding and non-ASCII Docs Assembler folder names. Do not rename `Ξ ...`, `δ steps`, or `Ω variables` folders unless the user specifically asks.
- Do not reintroduce a root `_config.yml`; Pages builds from `docs/_config.yml`.
- Keep links valid from their rendered location. Fragment pages under `docs/*_frags/` usually need `../section-name/` links to reach top-level guide pages.

## Validation Checklist

Before claiming a runbook or publish fix is complete:

1. Run `git status --short --branch`.
2. Check for stale bad patterns with `rg` when the task names a specific fact or URL.
3. Verify local internal links for changed Markdown/Docs Assembler pages.
4. If changes are committed and pushed, confirm the GitHub Pages workflow completes successfully.
5. Smoke-test the live Pages URLs affected by the change.

Known live site:

- `https://gitcak.github.io/TC_Runbook/`

Useful API check:

```powershell
Invoke-WebRequest 'https://api.github.com/repos/gitcak/TC_Runbook/actions/runs?per_page=5' -UseBasicParsing
```

## Host Facts Used by the Runbook

When reviewing factual consistency against the validated local host, these are the expected baseline values:

- Host: `server2019tc`
- Teamcenter root: `C:\TC2412`
- Teamcenter data: `C:\tcdata`
- Base release: `2412`
- Installed full version: `2412.0.0.8`
- Patch/about version: `2412.8`
- Patch package label: `2412.008`
- SQL Server: default `MSSQLSERVER` on port `1433`
- IIS site/app: `Default Web Site` with `/tc`
- App pool: `TcWebTierPool`
- Server Manager service: `Teamcenter Server Manager TCFISHER_PoolA`
- Server Manager ports: `8086`, `8087`, `8088`
- AWC gateway: `http://server2019tc:3000`
- AWC gateway `/tc` target: `http://server2019tc/tc`

Verify these from the machine before changing runbook claims. Good evidence sources include:

- `C:\TC2412\install\configuration.xml`
- `C:\TC2412\pool_manager\confs\TCFISHER\serverPool.properties`
- `C:\TC2412\microservices\gateway\config.json`
- `Get-Service`
- `Get-NetTCPConnection`
- IIS `WebAdministration` cmdlets

## Git and Publishing

- Main branch is `main`; remote is `https://github.com/gitcak/TC_Runbook.git`.
- GitHub Pages publishes from the workflow, not from a local `pub/` folder.
- If a user asks to publish, commit only relevant files, push `main`, wait for the Pages workflow, then verify the live URL.
- Avoid broad cleanup commits. Keep runbook content, source-map edits, and publish/config changes easy to review.

## Claude Code Coexistence

- Claude Code may create or use `CLAUDE.md`; do not treat that as a replacement for this shared agent guide unless the user asks.
- If both files exist, keep operational repo facts aligned and avoid contradictory instructions.
- Prefer short, actionable repo instructions over chat-history summaries. Put durable project rules here; put session-specific findings in appropriate docs such as `docs/FACTUAL_CONSISTENCY_REVIEW.md`.
