# Engineering Overview — How BlackIce Was Built

This document describes the product's implementation approach and architecture. It is not a step-by-step build or installation guide.

## 1. Application foundation

The BlackIce desktop clients are written in C# for `net8.0-windows` and use Windows Presentation Foundation (WPF) for the desktop UI. The clients are built as Windows x64 applications with administrator execution level because firewall policy changes require elevated Windows permissions.

The English and German applications are separate localized client variants. Their UI text and language-specific build guardrails are maintained independently while the feature baseline is kept aligned. The main client code is concentrated in `src/Program.cs`, with internal service types for firewall operations, DNS resolution, LAN context, application data and licensing.

## 2. Windows Firewall integration

BlackIce deliberately uses the Windows Firewall engine rather than shipping its own network filter driver.

- The application reads firewall rules and active profiles through Windows Firewall management tools.
- Rule creation, updates and removal are issued through the Windows `NetSecurity` PowerShell cmdlets and `netsh advfirewall` where appropriate.
- For sensitive operations, the code checks process exit/error state and reads the resulting local rule state back from Windows.
- Multi-address operations use bounded batches and include targeted verification and rollback/cleanup paths.
- The program is elevated because the underlying Windows operations require administrator permissions.

This design keeps enforcement inside Windows. It also means BlackIce behavior is subject to Windows policy precedence, Group Policy, permissions and the state of the local Firewall service.

## 3. Network information and telemetry

BlackIce combines several Windows and .NET data sources instead of treating every source as a complete packet-level truth:

| Information | Implementation source | Interpretation |
|---|---|---|
| Active TCP sessions | .NET `IPGlobalProperties` / `System.Net.NetworkInformation` | Current TCP table snapshot, not a full packet capture. |
| LAN neighbour context | Windows neighbour cache (`Get-NetNeighbor`) with ARP fallback | A cached neighbour is not proof of an active application session; the UI distinguishes discovered peers from confirmed TCP sessions. |
| DNS cache and host-level DNS events | Windows DNS Client cmdlets and Operational event `3008` | Host-wide DNS context; process attribution is not guaranteed. |
| Process-aware DNS context | Sysmon Operational event `22`, when available | Optional source; requires Sysmon installation and configuration. |
| Blocked connection events | Windows Security / Windows Filtering Platform event `5157` | Visibility depends on Windows failure-auditing policy. An event can be caused by any applicable firewall policy, not necessarily only the Kill Switch. |
| Process metadata | Windows process/WMI information | Supplementary context for a locally observed connection. |

The application does not silently turn on the relevant Windows audit policies. This avoids making a system-wide audit-policy change without an explicit operator decision.

## 4. Local state and credential handling

The client uses SQLite-compatible storage components, including SQLCipher support, for local data. Windows registry and DPAPI protections are used for machine-level secrets such as NOVA credentials and database-protection material in the relevant components.

The local-first design avoids a required BlackIce backend. It also means the data and logs remain on the managed PC unless the operator explicitly exports or transmits them through another application.

The UI's IP Mask is a presentation feature only. It should not be interpreted as sanitization of database contents, logs, network packets, clipboard data or exported screenshots.

## 5. Separate offline License Manager

The Admin License Manager is a separate WPF application targeting `net8.0-windows`. It is designed as an offline issuer rather than a web service.

### Request and issuance flow

1. The customer client creates a `.blreq` request using the `BIREQ1` request envelope. It includes customer identity, e-mail, hardware ID, license type, requested duration and request metadata.
2. The e-mail action opens a draft addressed to the configured support recipient and attaches the request file. It does not silently send the e-mail.
3. The administrator imports the request, reviews the customer and hardware data, chooses USER or DEV, and confirms or changes the requested term.
4. The Admin License Manager signs the license payload using the protected RSA private key and records issuance data in the encrypted local database.
5. The customer enters the `.blic`/`BI2` token. The client validates the RSA-PSS/SHA-256 signature, product/schema, issue time, expiry and hardware binding locally with the public key.

### Vault design described by the source

- The local licensing database uses SQLCipher page encryption.
- The database key is protected with Windows DPAPI in the configured machine scope.
- The RSA private key is stored as an encrypted PKCS#8 envelope using AES-256-GCM.
- The master password is processed with PBKDF2-HMAC-SHA-256.
- A portable `.bivault` recovery package encrypts the recovery payload and validates integrity before restore.

These are implementation details, not a claim of independent security certification. The current design has explicit operational limitations: DPAPI material is machine-bound outside the recovery workflow; offline licenses cannot be centrally revoked instantly; a lost master/recovery password cannot be recovered by the application; and the source has not undergone an independent security audit.

## 6. Design and development history

BlackIce evolved through incremental, feature-scoped releases rather than a single monolithic rewrite. The work concentrated on a consistent desktop control surface while retaining Windows as the policy enforcement layer.

The development sequence established several recurring practices:

- **Feature increments:** firewall rule handling, network zones, connection visibility, DNS context, Kill Switch, application rules and licensing were added and refined in separately documented increments.
- **EN/DE parity:** language-specific UI and build checks were maintained for both client variants.
- **Guardrails:** preflight checks were added to detect missing source files, stale API assumptions, localization leakage and changes to critical implementation markers.
- **Verified operations:** rule changes were followed by state checks, with rollback or cleanup code for selected multi-step operations.
- **Explicit limits:** telemetry dependencies, IP-based domain blocking, Win32-only app rules and the offline nature of licensing are documented rather than described as capabilities the product does not have.
- **Separate license authority:** the customer UI does not contain the license-signing private key; issuance is kept in the standalone Admin License Manager.

The repository baseline documented here is client `29.14.4`, Admin License Manager `1.0.5`, release builder `1.0.7`, and client UI integration `UI Fix 27`.

## 7. Product development sequence

The repository changelog shows a feature-led progression. The milestones below describe the development direction, not a claim that every possible Windows configuration has been certified.

| Development area | Engineering work represented in the source history |
|---|---|
| Firewall foundation | Centralized rule inventory and change operations, profile awareness, and Windows-native rule management. |
| Network context | Active TCP views, LAN neighbour-cache context, DNS lookups and event-backed DNS history. |
| Internet control | Manual IPv4/IPv6 Kill Switch, explicit local/intranet scope handling, rule verification and rollback-oriented updates. |
| Visibility and diagnostics | WFP block-event presentation, Cyber Terminal commands, System Logs, Statistics and process context where Windows provides it. |
| Desktop usability | Dark visual system, custom window controls, responsive layouts, faster dialogs, IP display masking and EN/DE parity. |
| Licensing | Customer request form, offline Admin License Manager, signed V2 tokens, encrypted vault storage and portable recovery. |
| Integration baseline | UI Fix 27 preserves the UI Fix 21 client layout while restoring the original customer-side duration selector and keeping the Admin License Manager at 1.0.5. |

This history is reflected in the `UIFIX*`, `FEATUREFIX*`, `PREFLIGHT_*` and component changelog records kept with the source.

## 8. Current validation boundary

Source archive integrity and package composition were checked during the GitHub documentation update. That is not equivalent to a Windows build or an end-to-end runtime test. Before a customer release, the following still require verification on a Windows test machine:

- Native EN and DE compilation and startup.
- Installer install, upgrade and uninstall behavior.
- Firewall rule create/update/delete and rollback behavior across Domain, Private and Public profiles.
- Kill Switch behavior for IPv4, IPv6, local LAN and external Internet destinations.
- WFP/DNS telemetry behavior with the relevant audit logs both enabled and unavailable.
- License request, import, admin review, signing, activation, expiry and Lifetime behavior.
- Vault backup and recovery on a replacement Windows PC.

## 9. Source security restriction

The current client source retains legacy licensing and cryptographic compatibility constants. The repository must remain private until those compatibility paths are migrated, removed or redesigned and a focused source/binary security review has been completed. See [`PUBLIC_RELEASE_BLOCKER.md`](../PUBLIC_RELEASE_BLOCKER.md).
