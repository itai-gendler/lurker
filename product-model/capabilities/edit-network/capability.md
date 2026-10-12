---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
domain: networks
---

# Edit network

Supplied owned configuration saved.

Supplied fields are saved. Configuration editing does not imply an immediate reconnect; host changes are checked against policy.
