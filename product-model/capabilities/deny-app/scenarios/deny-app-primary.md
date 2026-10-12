---
kind: primary
routes:
  web: Web
steps:
- text: The User invokes deny app.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::oauth-approval
  actor: user
- text: Denial returns without issuing access
  kind: product
  entities:
  - entity: client-application
    effect: reads
    facts:
    - Name
    - Website
    - Return locations
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: vue_client/src/views/OAuthAuthorize.vue
---

# Deny app

## Trigger

The User invokes deny app.

## Outcome

Denial returns without issuing access

Denial returns access_denied or its out-of-band result without creating access. Denial occurs before the approval-only displayed-account comparison.
