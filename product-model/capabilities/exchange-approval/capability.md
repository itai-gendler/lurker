---
availability:
- place: oauth
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts#consumeCode
---

# Exchange approval

Bound, valid code and PKCE verifier produce access.

Exchange consumes the code before later client, return-location and PKCE validation. Success issues OAuth access without an automatic expiry or refresh token.
