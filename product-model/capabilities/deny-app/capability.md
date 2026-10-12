---
availability:
- place: web::personal
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: vue_client/src/views/OAuthAuthorize.vue
---

# Deny app

Denial returns without issuing access.

Denial returns access_denied or its out-of-band result without creating access. Denial occurs before the approval-only displayed-account comparison.
