# lufulus-online-client

Public distribution channel for the **Lufulus Online** Windows game client.

The client **binaries** are published as **GitHub Releases** (one per version); this
git tree holds only small text indexes that a launcher/updater reads:

| Path | Purpose |
|---|---|
| `manifest/latest.json` | The current release pointer: version, download URL, SHA-256, `mandatory` (forced) flag, `minClientBuild`, `minLauncherVersion`. |
| `manifest/versions/<version>.json` | Immutable per-version snapshot of the manifest (history). |
| `manifest/repair-manifest.json` | Per-file SHA-256 + size for the latest release, used by the launcher to verify/repair an install. |

## Stable download URLs

- Latest client zip: `https://github.com/golgufus/lufulus-online-client/releases/latest/download/lufulus-online-client.zip`
- Latest repair manifest: `https://github.com/golgufus/lufulus-online-client/releases/latest/download/repair-manifest.json`
- Latest manifest (raw): `https://raw.githubusercontent.com/golgufus/lufulus-online-client/main/manifest/latest.json`

## How it is published

The source lives in the private `golgufus/lufulus` repo. Its publish pipeline builds the
self-contained client, then `scripts/Publish-ClientToGitHub.ps1` creates the GitHub Release
and pushes the updated manifests here. golgufus.com redirects its download button to the
Release asset above; a local copy is kept in lufulus' own `publish/` folder as a backup.

## Launcher (coming)

A standard console launcher will read `manifest/latest.json`, compare the installed version,
and install/upgrade/repair under the protocol documented in the `lufulus` repo
(`docs/client-launcher-protocol.md`). Upgrades are **forced by default**; a release may opt
out by setting `mandatory: false`.
