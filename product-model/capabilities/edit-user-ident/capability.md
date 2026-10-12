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
domain: administration-users
---

# Edit user ident

Ident override assigned or cleared.

Standalone ident assignment validates format and effective uniqueness. Clearing returns to the effective default. Changes apply on a subsequent connection, without an automatic reconnect.
