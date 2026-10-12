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

# Export network certificate

Owned certificate and private credential exported.

The certificate and private credential are returned through the qualified owned download with no-store handling.
