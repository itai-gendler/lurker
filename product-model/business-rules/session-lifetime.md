---
appliesTo:
- type: entity
  id: session
references:
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# Session lifetime

Ordinary sessions expire thirty days after issuance. Lookup removes expired rows; logout removes the presented session. This lifetime is not copied to API tokens or OAuth access, and row removal is not a global already-authenticated-socket termination promise.
