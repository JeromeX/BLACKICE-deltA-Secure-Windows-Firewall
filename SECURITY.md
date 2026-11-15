# Security Policy

## Scope

This repository is a public-facing product and documentation space. It contains product information, screenshots and diagrams; it does not contain the BlackIce application source code, executable releases or confidential internal tools.

## Reporting a security issue

Do not publish exploit details, personal information, customer logs, hardware identifiers, license tokens, API credentials, private network details or other sensitive data in a public issue.

Use GitHub's **Private vulnerability reporting** feature when enabled. If it is unavailable, contact the repository maintainer through a private channel listed in the repository owner's profile. Include only the minimum information needed to understand the report.

## Screenshot and documentation hygiene

- Mask public IP addresses, private network details and customer identifiers before adding screenshots.
- Do not include terminal output containing credentials, tokens or host-specific secrets.
- The BlackIce IP Mask is a display aid and must not be treated as a general-purpose data-sanitization tool.
- Do not upload application databases, diagnostic exports or customer support files to this repository.

## Product security boundaries

- BlackIce manages the built-in Windows Defender Firewall; Windows remains responsible for packet filtering.
- Windows event/audit settings affect the availability of some diagnostic information.
- Product documentation describes known limitations and does not claim independent security certification.
