---
entities:
- entity: invite
  shows:
  - Expires at
  - Redeemed at
  - Validity
  collects:
  - Expires at
- entity: account
  shows:
  - Username
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
entryPoints:
- web: /admin/invites
---

# Invites

Invitation validity, expiry, issuer/redeemer. Collects expiry choice/deletion.
