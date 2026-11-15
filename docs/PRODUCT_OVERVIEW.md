# BlackIce Δ — Product Overview

## Product identity

BlackIce Δ is a Windows desktop control and visibility application for the built-in Windows Defender Firewall. Its purpose is to make local firewall policy, network zones, IP controls, application rules and connection context easier to inspect and manage from one workspace.

It is a Windows administration product, not an independent packet-filter driver. Windows Defender Firewall remains the enforcement engine.

## Intended use

BlackIce is designed for technically capable Windows users and administrators who want a consolidated view of local firewall configuration and network activity without relying on a remote BlackIce control plane.

Typical use cases include:

- Reviewing active Windows Firewall profiles and local rules.
- Creating or removing supported program and IP rules.
- Applying a deliberate Internet-only Kill Switch while preserving defined local/intranet scopes.
- Reviewing active TCP sessions, local peers and available DNS context.
- Inspecting application logs and running basic network diagnostics.

## Product pillars

### Native Windows enforcement

BlackIce manages rules in Windows Defender Firewall. Its integration uses Windows administration surfaces such as the NetSecurity PowerShell module and netsh advfirewall. The program reports failures and verifies selected changes instead of claiming success solely because a command was started.

### Network context, not packet-content inspection

The interface can correlate active TCP information, process metadata, neighbour-cache entries, DNS cache and available Windows event data. It does not decrypt TLS sessions or inspect application payload content.

### Local-first operation

Core firewall management is performed against the local Windows machine. This product baseline does not require a BlackIce cloud service or remote policy server. Optional NOVA AI is a separate, operator-configured integration.

### Bilingual product

The repository documents English and German client variants. The language-specific variants are kept aligned around a common functional baseline.

## Feature groups

| Group | Product functions |
|---|---|
| Firewall control | System Rules, Network Zones, App Blocking, Blocked IPs, Allowed IPs, Internet Kill Switch |
| Network insight | Connections, LAN peer context, DNS diagnostics, System Logs, Statistics, Cyber Terminal |
| Privacy and configuration | UI-only IP Mask, System Settings, optional NOVA AI configuration |

## Important boundaries

- Domain blocking uses current resolved A/AAAA addresses and behaves as IP blocking, not a continuously maintained DNS-name rule.
- Classic Win32 executable paths are supported for App Blocking; package-identity rules for Store/MSIX applications are not implemented.
- WFP event 5157 is visible only when the corresponding Windows auditing is configured. BlackIce does not enable that policy automatically.
- Windows DNS Client event 3008 is host-level context. Sysmon event 22 is optional and only useful when Sysmon is installed and configured.
- The IP Mask is display-only. It does not alter traffic, persisted logs or files outside the relevant UI rendering path.

## Current product baseline

- Client version: 29.14.4 (English and German)
- Client UI baseline: UI Fix 27, based on UI Fix 21

This overview describes the documented product baseline, not an independently certified security product.
