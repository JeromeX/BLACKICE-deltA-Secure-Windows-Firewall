# BlackIce Offline License Workflow

## Components

- **Customer client:** creates a `.blreq` request and later verifies a signed token.
- **Admin License Manager:** separate offline WPF application; imports requests, reviews license terms and signs tokens.
- **Encrypted vault:** local SQLCipher database, protected database key, encrypted RSA private-key envelope and recovery metadata.
- **Customer token:** signed `BI2` payload delivered to the customer and activated locally.

## Request terms

| Code | Term | Displayed value |
|---|---|---:|
| `7` | 7 days | Free Trial |
| `30` | 30 days | Free Trial |
| `365` | 1 year | €25 |
| `730` | 2 years | €45 |
| `LIFETIME` | Lifetime | €100 |

The client defaults a new request to 365 days. This default is independent from an already-installed license. An installed Lifetime license can therefore show `LIFETIME` as its expiry status while the selector for a new request still displays `1 year`.

The admin manager imports the requested duration and allows the administrator to review or change it before signing. Prices are labels/request metadata only; no payment processor, invoice generator or payment reconciliation service is included.

## Data flow

1. Client serializes request metadata into a `BIREQ1` `.blreq` file.
2. Client creates an e-mail draft to `support@meerheimatliebe.de` with the request attached.
3. Customer reviews and sends the draft manually.
4. Admin imports the file and checks identity, e-mail and hardware binding details.
5. Admin chooses `USER` or `DEV`, confirms duration and signs.
6. Admin returns the signed license token to the customer.
7. Client verifies the token locally using RSA-PSS/SHA-256, product/schema validation and hardware binding.

## Security and operational limits

- No online license server is required for activation.
- No central instant revocation or online activation-seat management is available.
- The public verification key may be distributed; the private signing key must remain in the protected admin vault.
- E-mail address ownership is not independently verified by an online challenge in this offline workflow; the administrator must review the request and recipient details.
- Recovery requires the correct recovery password and original master password. The application cannot recover either password if it is lost.
