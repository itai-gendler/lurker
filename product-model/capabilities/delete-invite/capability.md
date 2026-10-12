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
domain: administration-invites
---

# Delete invite

Invitation removed.

Removing an invitation does not remove the admitted member or revive a consumed proof.
