---
kind: validation
routes:
  web: Web
steps:
- text: The User approves the displayed application after the browser has changed to a different member identity.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::oauth-approval
  actor: user
- text: Approval refused when cookie account differs from displayed account
  kind: product
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts: *id001
  actor: user
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

# Approve app account changed

## Trigger

The User approves the displayed application after the browser has changed to a different account.

## Outcome

Approval refused when cookie account differs from displayed account
