---
references:
- kind: code
  role: implementation
  target: server/db/webauthnCredentials.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
---

# Passkey

An individually named registered WebAuthn credential belonging to an account.

## Information kept

- **Label** — The person’s displayed label for this saved subject.
- **Registration** — Registered credential or downstream registration information appropriate to this subject.
- **Device information** — Observed passkey device and credential information.
- **Created at** — When this saved subject was created.
- **Last used at** — Most recently recorded credential or authorization use.

## States

### Registered

An individually named registered WebAuthn credential belonging to an account.
