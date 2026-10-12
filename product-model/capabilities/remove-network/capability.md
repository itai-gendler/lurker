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

# Remove network

Connection disposed; network and dependent data removed.

The live connection is disposed before the network and its dependent retained data are deleted.
