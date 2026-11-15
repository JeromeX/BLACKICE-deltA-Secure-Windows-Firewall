# BlackIce Δ v29.14.4 — UI Fix 27

## Release contents

- English Windows client `v29.14.4`.
- German Windows client `v29.14.4`.
- BlackIce License Manager – Admin Edition `1.0.5`.
- Complete release builder `1.0.7`.

## Highlights

- Preserves the UI Fix 21 client layout and surrounding firewall/network features.
- Restores the original customer-facing duration/price selector in the embedded License Manager page in EN and DE.
- Supports request terms of 7 days, 30 days, 1 year, 2 years and Lifetime.
- Defaults a new request to 1 year / 365 days and writes the selected term into the BIREQ1 `.blreq` payload.
- Keeps the current license status separate from the requested duration for a future license. A current Lifetime license does not automatically change the new-request selection.
- Includes the donor Admin License Manager 1.0.5 with offline encrypted storage and signed V2 licensing.

## Build artifacts

Run `Build-All-BlackIce.ps1` on Windows as described in `README-COMPLETE-BUILD.md`. The script produces the Admin setup and portable package, EN setup and client ZIP, DE setup and client ZIP, plus a combined release archive and SHA-256 manifests.

## Validation note

This source package has been structurally checked. Native Windows build, installer, firewall, vault recovery and end-to-end licensing tests must be completed before distributing these artifacts to customers.

## Distribution restriction

The current source retains legacy V1 license verification for migration. Do not publish this source or its compiled client binaries publicly until the blocker in `PUBLIC_RELEASE_BLOCKER.md` has been resolved.
