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
  target: server/db/invites.ts
domain: administration-invites
---

# Create invite

Expiring invitation issued.

A positive supported expiry creates an invitation; the default is seven days.
