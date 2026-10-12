---
references:
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# Session

An opaque ordinary sign-in credential accepted on its supported cookie or bearer surfaces.

## Information kept

- **Credential** — The opaque ordinary session token.
- **Issued at** — When the ordinary session was issued.
- **Expires at** — The ordinary credential’s fixed 30-day expiry; request authentication requires it unexpired, without a promise to reauthenticate every already-open socket.

## States

### Issued

An opaque ordinary sign-in credential accepted on its supported cookie or bearer surfaces.
