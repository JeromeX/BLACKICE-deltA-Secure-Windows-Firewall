# BlackIce Δ — Changelog

## GitHub product documentation refresh — 2026-11-15

- Reworked the repository front page into a product overview rather than a build guide.
- Added functional, architecture and offline-licensing SVG diagrams plus a redacted UI screenshot.
- Added product and engineering overviews that describe the implementation, development approach and actual limitations.
- Replaced the missing-license placeholder with a proprietary all-rights-reserved notice containing a legal copyright-holder field that must be completed by the rights holder.
- Expanded the private-repository blocker to include known legacy V1, fixed-key crypto and database-migration compatibility material.
- No client source code or runtime behavior was changed in this documentation update.


## v29.14.4 / Release Builder 1.0.7 — GitHub source baseline UI Fix 27

### Client and UI
- Preserves the UI Fix 21 application layout and surrounding firewall features.
- Restores the original customer-facing License Manager duration/price selector in both EN and DE clients (UI Fix 27).
- Provides 7-day, 30-day, 1-year, 2-year and Lifetime request terms.
- Keeps 1 year / 365 days as the default for a new request.
- Serializes the selected request term into the BIREQ1 `.blreq` payload and the e-mail draft.
- Keeps current-license status and the requested term for a future license separate. An active Lifetime license does not automatically change a new-request selection.

### Admin licensing
- Bundles BlackIce License Manager – Admin Edition 1.0.5.
- Supports USER and DEV license types and the same five validity options.
- Imports the requested term from `.blreq`; an administrator may review or change it before signing.
- Uses the encrypted offline vault and V2 RSA-PSS/SHA-256 license verification flow.

### Release tooling
- Complete builder version 1.0.7 coordinates the Admin License Manager and EN/DE client release builds.
- Produces setup installers, binary client ZIPs, a combined release ZIP and SHA-256 manifests on Windows.

### Validation boundary
- Source archive integrity and package structure were checked during preparation.
- Native Windows compilation, installer execution, firewall behavior, vault recovery and end-to-end license issuance/activation still require verification on a Windows machine.

## Historical notes

The detailed file `CHANGELOG_1.0.7.md` records earlier implementation stages. Some earlier entries describe a temporary 7-/30-day-only license configuration. Those entries were superseded by UI Fix 27, which restores the five duration/price choices listed above. The current integrated package baseline is UI Fix 27, not the UI Fix 28 dropdown-selection experiment.
