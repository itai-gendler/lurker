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

# Set network certificate

Valid generated/imported certificate pair attached.

A generated or imported matching certificate/private-key pair is attached to a TLS-enabled network and used on a subsequent connection.
