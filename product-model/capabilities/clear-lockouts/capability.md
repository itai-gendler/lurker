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
  target: server/middleware/rateLimit.ts
domain: administration-lockouts
---

# Clear lockouts

Current blocked entries lifted.

Currently blocked entries are lifted; subthreshold failure budgets are retained.
