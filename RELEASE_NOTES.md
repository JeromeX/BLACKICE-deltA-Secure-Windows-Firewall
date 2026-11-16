# BlackIce Δ v29.14.4 — Public Product Preview

**Release type:** Product presentation and documentation only  
**Tag:** `v29.14.4-public-preview`  
**Client baseline described:** v29.14.4 · UI Fix 27  
**Languages:** English and German

## Overview

This public preview introduces the BlackIce Δ product presentation repository. It documents the Windows desktop client, its user-facing feature set, product architecture and supported diagnostic views.

BlackIce Δ provides a visual management and visibility layer for the built-in Windows Defender Firewall. Windows Defender Firewall remains the packet-filtering engine; BlackIce does not ship an independent packet-filter driver.

## Product areas

- Windows Firewall rule inspection and management
- Network Zones and firewall profile visibility
- Application blocking for supported Win32 executable paths
- Blocked and allowed IP lists
- Manual IPv4/IPv6 Internet Kill Switch, designed to preserve local/intranet connectivity
- TCP connection and LAN neighbour context
- DNS diagnostics and available Windows DNS telemetry
- System Logs, Cyber Terminal and Statistics
- UI-only IP Mask
- English and German localized user interface

## Screenshots and diagrams

The repository includes a gallery of 17 BlackIce client screenshots and two product diagrams:

- [Screenshot gallery](docs/SCREENSHOTS.md)
- [Feature map](docs/assets/blackice-feature-map.svg)
- [Client architecture](docs/assets/blackice-architecture.svg)

## Planned license pricing — not yet released

The following are planned display values only. Paid terms are **not released, not available for purchase and not an approved public offer**.

| Planned term | Planned price | Status |
|---|---:|---|
| 7 days | Free Trial | Trial option |
| 30 days | Free Trial | Trial option |
| 1 year | €25 | **NOT YET RELEASED** |
| 2 years | €45 | **NOT YET RELEASED** |
| Lifetime | €100 | **NOT YET RELEASED** |

## What this release does not contain

This is a documentation/product-preview release, not an application distribution:

- No BlackIce client source code
- No EXE, DLL, installer or customer binary package
- No internal administrative licensing tools
- No private signing keys, credentials, license databases or customer data

The separate internal License Manager is intentionally excluded from this public repository and this release.

## Validation and status

This release publishes product information, screenshots and diagrams only. It does **not** certify the application or claim that a customer build has passed native Windows compilation, installer, firewall-behavior or end-to-end runtime testing.

For technical boundaries and known limitations, see the [engineering overview](docs/ENGINEERING_OVERVIEW.md) and [product overview](docs/PRODUCT_OVERVIEW.md).
