---
availability:
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
---

# Unregister push device

Registration matching owner and endpoint removed.

Deregistration matches owner plus endpoint without an additional transport predicate.
