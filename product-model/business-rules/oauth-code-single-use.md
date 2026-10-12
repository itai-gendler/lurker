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

# OAuth code single use

An approval code lasts ten minutes. Exchange consumes the code on lookup before client/return-location/PKCE checks, so failed later validation does not leave a retryable code.
