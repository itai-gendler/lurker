---
kind: primary
routes:
  web: Web
steps:
- text: The User invokes approve app.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::oauth-approval
  actor: user
- text: Cookie account matching the displayed account approves and receives an authorization code
  kind: product
  entities:
  - entity: authorized-app
    effect: creates
    facts:
    - Approval
    - Issued access
    - Last used at
    to: Approved
  - entity: client-application
    effect: changes
    facts:
    - First approval
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

# Approve app

## Trigger

The User invokes approve app.

## Outcome

Cookie account matching the displayed account approves and receives an authorization code

The completion returns a ten-minute, single-use code to the accepted redirect or out-of-band result.
