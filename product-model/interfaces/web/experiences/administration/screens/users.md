---
entities:
- entity: account
  shows:
  - Username
  - Pause status
  - Ident
  - Retained history counts
  collects:
  - Ident
  - Pause status
- entity: recovery-link
  shows:
  - Expires at
  - Validity
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
entryPoints:
- web: /admin/users
---

# Users

Account roster, pause/ident/history counts and recovery-link metadata. Collects administration inputs.
