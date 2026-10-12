---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes revoke app access.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::authorized-apps
    client:
      place: client-api::personal
  actor: user
- text: Authorization and associated access/sockets revoked
  kind: product
  entities:
  - entity: authorized-app
    effect: removes
    from: Approved
  - entity: web-push-subscription
    effect: removes
    with: authorized-app
  - entity: native-push-device
    effect: removes
    with: authorized-app
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
  target: server/services/wsHub.ts
---

# Revoke app access

## Trigger

The User invokes revoke app access.

## Outcome

Authorization and associated access/sockets revoked

Application revocation removes associated codes/tokens and push registrations and closes associated WebSocket access.
