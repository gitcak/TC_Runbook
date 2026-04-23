# TC_Runbook

Standalone Docs Assembler and Jekyll source for the Teamcenter 2412 installation runbook.

This repository is scoped to `C:\TC_Runbook` only. It does not vendor `C:\TC_AI`, and the checked-in workspace file has been trimmed so the repo can stand alone.

## Repository Layout

- `tsmaps/` contains the Docs Assembler source maps and shared variables.
- `docs/` contains the authored Jekyll pages.
- `pub/` is generated output and is intentionally ignored.
- `.bin/` is local Docs Assembler working state and is intentionally ignored.

## GitHub Pages

This repo is configured as a project Pages site deployed from GitHub Actions on the `main` branch.

- Workflow: `.github/workflows/pages.yml`
- Jekyll base path: `_config.yml` uses `baseurl: "/TC_Runbook"`
- Docs Assembler git metadata: `docs-assembler-config.json` uses repo `TC_Runbook` on branch `main`

If you publish this under a different GitHub repository name, update:

1. `_config.yml` `baseurl`
2. `docs-assembler-config.json` `gitConfig.repo`
3. `docs-assembler-config.json` `gitConfig.publishUrl`

If the site will live under a GitHub user or organization site root instead of a project repo, also set `_config.yml` `url` and adjust `baseurl` accordingly.

## First Push

1. Create a GitHub repository named `TC_Runbook`.
2. Add it as `origin`.
3. Push `main`.
4. In GitHub repository settings, set Pages to use GitHub Actions.

After the first push, the Pages workflow will build the Jekyll site from the repository root and deploy it.
