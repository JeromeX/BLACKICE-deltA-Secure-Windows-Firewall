# Public Release Blocker — Private Repository Required

**Status: BLOCKED for public source publication and public binary distribution.**

The current BlackIce v29.14.4 / UI Fix 27 source baseline contains legacy licensing and cryptographic compatibility material. A public release must not be made from this source state.

## Known items requiring remediation

1. **Legacy V1 license verifier:** both EN and DE clients retain a legacy V1 compatibility path, including shared verification material embedded in client code. A public source or binary release would disclose this mechanism and its embedded material.
2. **Legacy fixed-key application crypto:** the client source still contains a fixed AES key/IV in the legacy `CryptoStore` compatibility helper. This is not an appropriate pattern for protecting new secrets and should be retired after affected stored data has been migrated.
3. **Legacy database migration credential:** the client retains a hard-coded legacy database password for migration of old local database files. It must be treated as exposed compatibility material, not as a current security boundary.
4. **No independent review:** the current source and vault design have not received an independent security audit or formal threat model.

These are source-level compatibility findings. The actual customer vault database, DPAPI key files, private RSA signing key, recovery packages and API credentials were not included in the prepared source archive, but that does not make the source safe for public release.

## Required work before public release

1. Inventory all deployed V1 licenses and legacy local database formats.
2. Migrate existing customers and data without losing valid activation or user data.
3. Remove the legacy V1 verifier and shared verifier material from both language clients once migration is complete.
4. Retire the fixed-key legacy crypto helper and hard-coded legacy database migration credential after the required migration path is safely handled.
5. Replace compatibility paths with modern per-installation or per-record key management where encryption is still required; do not simply move constants into another source file.
6. Add build guardrails that fail when any retired constants or compatibility paths reappear.
7. Rebuild EN and DE on Windows and inspect source and produced binaries for embedded secrets and credentials.
8. Test V2 issuance, activation, expiry, Lifetime behavior, invalid-token rejection, migration, recovery and rollback on Windows.
9. Have the resulting design and release artifacts reviewed independently before changing repository visibility.

## What is safe to distribute in the V2 model

The V2 client verifier uses a public key, which is intended to be embedded in clients. The RSA private signing key must remain in the protected Admin License Manager vault and must never be copied into the client or committed to Git.

The public verification key being distributable does not neutralize the separate legacy issues listed above.

## Current handling

- Keep the repository private.
- Do not upload public release binaries built from this source state.
- Do not disable V1 compatibility until existing customer migration has been verified.
- Do not commit any customer vault, DPAPI key, database, recovery package, API credential, signed license or `.blreq` request.
