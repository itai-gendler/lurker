---
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
---

# Network certificate

The currently attached certificate and private credential used for an owned network’s TLS client authentication.

## Information kept

- **Certificate description** — Certificate information shown without disclosing its private credential.
- **Certificate** — The attached public TLS client certificate.
- **Private credential** — The attached private key available only through the qualified owned export or execution path.

## States

### Attached

A certificate and private-key pair is attached to the selected owned Network for subsequent TLS client authentication.
