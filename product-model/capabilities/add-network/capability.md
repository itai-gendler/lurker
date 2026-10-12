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

# Add network

Configuration saved and initial connection requested.

The valid name, host and nick configuration is saved and an initial connection is requested. An accepted request does not guarantee completed upstream registration.
