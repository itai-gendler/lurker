---
availability:
- place: web::administration
- place: client-api::administration
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
domain: administration-users
---

# Revoke recovery link

Outstanding recovery link invalidated.
