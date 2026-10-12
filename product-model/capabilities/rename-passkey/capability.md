---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
domain: account
---

# Rename passkey

Owned passkey label changes.
