# QLog Pro Ultimate

Offline-first PWA for facility / library logging, with local face recognition,
PP-OCR text extraction, QR scanning, reports and exports. No backend, no CDN,
no internet required after installation.

## Contents

| Path | Purpose |
|---|---|
| `index.html` | The entire application shell and logic |
| `install-gate.js` | Installation Password verification data (**generated at build time**) |
| `service-worker.js` | Offline precache + app shell fallback |
| `manifest.json`, `icons/` | PWA install metadata |
| `libs/`, `models/`, `fonts/` | Bundled offline dependencies |
| `scripts/generate-install-gate.mjs` | Build script that derives the installation verifier |
| `.github/workflows/deploy.yml` | Production build + GitHub Pages deployment |
| `QLog_Pro_Setup.md` | End-user setup notes |

## Two separate passwords

1. **Installation Password** — controlled by the system owner via the GitHub Actions
   secret `QLOG_INSTALLATION_PASSWORD`. Required once, on first run, before Superadmin
   Setup. Installers cannot create, change or reset it.
2. **Superadmin Password** — created by the installer after activation, used for daily
   access and changeable from inside the app.

> **Owners/admins: read [`INSTALLATION_PASSWORD_GITHUB_SETUP.md`](./INSTALLATION_PASSWORD_GITHUB_SETUP.md)**
> for the complete step-by-step guide to configuring the GitHub secret, rebuilding after
> a password change, verifying deployments, troubleshooting, and the pre-distribution
> checklist.

## Building / deploying

Push to `main` (or run the workflow manually from the **Actions** tab). The workflow
assembles the site, generates `install-gate.js` from the repository secret, verifies the
plaintext password never appears in the output, and deploys to GitHub Pages.

Local preview (the installation gate is skipped because no verifier is compiled in):

```bash
python3 -m http.server 8000
```
