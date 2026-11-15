# Engineering Overview — How BlackIce Was Built

This document describes the implementation approach and architecture of the BlackIce Windows client. It is not a step-by-step build or installation guide.

## 1. Application foundation

The BlackIce desktop clients are written in C# for net8.0-windows and use Windows Presentation Foundation (WPF) for the desktop UI. The clients are built as Windows x64 applications with administrator execution level because firewall policy changes require elevated Windows permissions.

The English and German applications are separate localized client variants. Their UI text and language-specific checks are maintained independently while the feature baseline is kept aligned. The primary client interface is organized around firewall operations, DNS resolution, LAN context, application data and diagnostics.

## 2. Windows Firewall integration

BlackIce deliberately uses the Windows Firewall engine rather than shipping its own network filter driver.

- The application reads firewall rules and active profiles through Windows Firewall management tools.
- Rule creation, updates and removal are issued through Windows NetSecurity PowerShell cmdlets and netsh advfirewall where appropriate.
- For sensitive operations, the application checks process exit/error state and reads the resulting local rule state back from Windows.
- Multi-address operations use bounded batches and include targeted verification and rollback/cleanup paths.
- The program is elevated because the underlying Windows operations require administrator permissions.

This design keeps enforcement inside Windows. BlackIce behavior is therefore subject to Windows policy precedence, Group Policy, permissions and the state of the local Firewall service.

## 3. Network information and telemetry

BlackIce combines several Windows and .NET data sources instead of treating every source as a complete packet-level truth:

| Information | Implementation source | Interpretation |
|---|---|---|
| Active TCP sessions | .NET IPGlobalProperties / System.Net.NetworkInformation | Current TCP table snapshot, not a full packet capture. |
| LAN neighbour context | Windows neighbour cache (Get-NetNeighbor) with ARP fallback | A cached neighbour is not proof of an active application session. |
| DNS cache and host-level DNS events | Windows DNS Client cmdlets and Operational event 3008 | Host-wide DNS context; process attribution is not guaranteed. |
| Process-aware DNS context | Sysmon Operational event 22, when available | Optional source; requires Sysmon installation and configuration. |
| Blocked connection events | Windows Security / Windows Filtering Platform event 5157 | Visibility depends on Windows failure-auditing policy. |
| Process metadata | Windows process/WMI information | Supplementary context for a locally observed connection. |

The application does not silently turn on the relevant Windows audit policies. This avoids making a system-wide audit-policy change without an explicit operator decision.

## 4. Local state and privacy

The client uses local application data to retain relevant settings and operational context. The exact information available depends on the module and Windows telemetry source.

The local-first design avoids a required BlackIce cloud backend. Data and logs remain on the managed PC unless the operator explicitly exports or transmits them through another application.

The UI's IP Mask is a presentation feature only. It should not be interpreted as sanitization of database contents, logs, network packets, clipboard data or exported screenshots.

## 5. Design and development history

BlackIce evolved through incremental, feature-scoped releases rather than a single monolithic rewrite. The work concentrated on a consistent desktop control surface while retaining Windows as the policy enforcement layer.

The development sequence established several recurring practices:

- **Feature increments:** firewall rule handling, network zones, connection visibility, DNS context, Kill Switch and application rules were added and refined in separately documented increments.
- **EN/DE parity:** language-specific UI and checks were maintained for both client variants.
- **Guardrails:** preflight checks were added to detect missing source files, stale API assumptions, localization leakage and changes to critical implementation markers.
- **Verified operations:** rule changes were followed by state checks, with rollback or cleanup code for selected multi-step operations.
- **Explicit limits:** telemetry dependencies, IP-based domain blocking, Win32-only app rules and Windows policy dependencies are documented rather than described as capabilities the product does not have.

## 6. Product development sequence

| Development area | Engineering work represented in the product history |
|---|---|
| Firewall foundation | Centralized rule inventory and change operations, profile awareness and Windows-native rule management. |
| Network context | Active TCP views, LAN neighbour-cache context, DNS lookups and event-backed DNS history. |
| Internet control | Manual IPv4/IPv6 Kill Switch, explicit local/intranet scope handling, rule verification and rollback-oriented updates. |
| Visibility and diagnostics | WFP block-event presentation, Cyber Terminal commands, System Logs, Statistics and process context where Windows provides it. |
| Desktop usability | Dark visual system, custom window controls, responsive layouts, faster dialogs, IP display masking and EN/DE parity. |

## 7. Current validation boundary

Product documentation and screenshot paths were checked against the repository. That is not equivalent to a Windows build or an end-to-end runtime test. Native compilation, installation, firewall behavior across network profiles, Kill Switch behavior for IPv4/IPv6 and available Windows telemetry still require verification on a Windows test machine before a customer release.

## 8. Product architecture

The architecture diagram and screenshot gallery describe the public-facing Windows client only. Internal administrative utilities and their implementation details are deliberately not part of this repository.
