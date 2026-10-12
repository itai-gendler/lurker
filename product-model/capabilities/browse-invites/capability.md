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

# Browse invites

Administrative invitation roster returned.

The administrative roster includes expiry, validity and issuer/redeemer association; consumed/expired rows remain until removed.
