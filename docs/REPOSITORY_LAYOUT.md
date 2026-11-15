# Repository layout

| Path | Purpose |
|---|---|
| `BlackIce_EN/` | English client source, assets, build script, Inno Setup installer definition and read-only test script |
| `BlackIce_DE/` | German client source, assets, build script, Inno Setup installer definition and read-only test script |
| `LicenseManager/` | Offline Admin License Manager source, storage, recovery, signing and client integration utilities |
| `Build-All-BlackIce.ps1` | Orchestrates the three component builds and complete release assembly |
| `README-COMPLETE-BUILD.md` | Detailed full build procedure and first-run signing-vault initialization |
| `PREFLIGHT_*`, `UIFIX*`, `COMPILEFIX*` | Existing validation markers and implementation notes consumed or referenced by build scripts |
| `.github/` | GitHub issue and pull-request templates |
| `docs/` | Current package metadata and repository/release workflow documentation |

The packaging task adds repository metadata and documentation only. The UI Fix 27 application source files and existing build scripts are kept from the selected base archive.
