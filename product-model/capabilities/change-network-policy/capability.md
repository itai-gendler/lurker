---
availability:
- place: web::administration
- place: client-api::administration
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
domain: administration-networks
---

# Change network policy

Instance host policy changes.

Validated network offering/policy changes retain a usable enabled preset when lockdown requires it.
