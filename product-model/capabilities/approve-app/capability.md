---
availability:
- place: web::personal
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: vue_client/src/views/OAuthAuthorize.vue
---

# Approve app

Cookie account matching the displayed account approves and receives an authorization code.

The completion returns a ten-minute, single-use code to the accepted redirect or out-of-band result.
