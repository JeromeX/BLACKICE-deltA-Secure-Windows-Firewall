# Contributing

This repository is a Windows application with privileged firewall and offline licensing components. Changes must be narrowly scoped and verifiable.

## Before proposing a change

- Open an issue using the supplied template and identify whether it affects EN, DE or both.
- Do not include customer identifiers, public IPs, license tokens, API keys, vault files or personal data.
- State the exact Windows version, PowerShell version, .NET SDK version and reproduction steps.

## Code changes

- Preserve parity between `BlackIce_EN` and `BlackIce_DE` unless a language-specific change is explicitly intended.
- Do not place private signing keys, vault data or provider API credentials in source code.
- Do not weaken firewall guardrails or silently change Windows Firewall policy.
- Keep build and preflight checks aligned with any source-level behavior change.
- Document user-visible behavior and any migration implications.

## Validation

For changes to firewall or licensing behavior, include the exact Windows test environment and observed results. Static source inspection alone is not an end-to-end validation.
