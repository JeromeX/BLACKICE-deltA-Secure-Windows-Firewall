# Security Policy

## Current release baseline

The source baseline documented here is BlackIce Δ `v29.14.4` / UI Fix 27 with Admin License Manager `1.0.5`.

**Repository visibility is restricted:** keep this source repository private until the legacy licensing and cryptographic compatibility material described in [`PUBLIC_RELEASE_BLOCKER.md`](PUBLIC_RELEASE_BLOCKER.md) has been removed or redesigned and a source/binary review has been completed.

## Reporting a vulnerability

Do not publish exploit details, license tokens, hardware identifiers, API keys, private keys, vault files, database files or customer network information in a public issue.

Use GitHub's **Private vulnerability reporting** feature when enabled. If it is unavailable, contact the repository maintainer through a private channel listed in the repository owner's profile. Include only the minimum information needed to understand and reproduce the issue.

## Sensitive material — never commit

- License Manager vault folders, private-key envelopes, DPAPI database-key files and `.bivault` recovery packages.
- Customer databases, `.blreq` requests, signed `.blic` tokens and hardware identifiers.
- NOVA AI API credentials, access tokens, mail credentials or private certificates.
- Production customer names, e-mail addresses, public IP lists, firewall exports or diagnostic logs containing personal/network information.
- Locally generated installers and build outputs unless explicitly approved for a release.

The `.gitignore` file provides baseline exclusions, but every staged change must be reviewed before commit.

## Security assumptions and limitations

- BlackIce delegates packet filtering to Windows Defender Firewall; Windows policy precedence and local administrator permissions remain relevant.
- WFP blocked-connection telemetry requires the relevant Windows audit policy.
- Offline licenses have no central instant-revocation channel.
- IP Mask is a UI presentation feature and is not a data-sanitization mechanism.
- The current source has not undergone an independent security audit or formal threat model.

## Public-release restriction

The current source contains legacy V1 verification and other fixed legacy crypto/database compatibility constants. These must not be exposed in a public source repository or public binaries. See [`PUBLIC_RELEASE_BLOCKER.md`](PUBLIC_RELEASE_BLOCKER.md). Do not disable migration compatibility until the impact on existing licenses and stored data has been assessed.
