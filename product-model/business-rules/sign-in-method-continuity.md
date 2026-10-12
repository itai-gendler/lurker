---
appliesTo:
- type: entity
  id: account
- type: entity
  id: passkey
references:
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/db/webauthnCredentials.ts
---

# Sign in method continuity

A personally removed password requires at least one passkey; removing a passkey requires another usable passkey or password. Administrator recovery has its separate proof-qualified replacement path.
