---
appliesTo:
- type: entity
  id: authorized-app
- type: entity
  id: account
- type: capability
  id: approve-app
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
---

# OAuth approval account match

Approval compares the actual cookie account with the account shown during approval and refuses a mismatch. Denial happens before this comparison and does not inherit it.
