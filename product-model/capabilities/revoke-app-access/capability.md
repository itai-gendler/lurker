---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
domain: authorized-apps
---

# Revoke app access

Authorization and associated access/sockets revoked.

Application revocation removes associated codes/tokens and push registrations and closes associated WebSocket access.
