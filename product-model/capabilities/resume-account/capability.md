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

# Resume account

Pause cleared; configured connections initialized.

Standalone resume clears pause and initializes configured connections; confirmed registration remains asynchronous.
