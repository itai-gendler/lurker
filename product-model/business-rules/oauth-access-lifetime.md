---
appliesTo:
- type: entity
  id: authorized-app
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
---

# OAuth access lifetime

OAuth access has no mapped automatic expiry or refresh token. Owner/app revocation and recovery remove evidenced access; scoped API-token rules are a separate credential contract.
