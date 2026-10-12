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

# Delete account

Permitted target’s live access and account/dependents removed.

Permitted account removal disposes live access before deleting dependent retained data. Self and final-administrator deletion are refused.
