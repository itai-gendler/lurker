---
kind: validation
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User attempts sign-in while the applicable failure throttle is blocking that request.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::login
    client-entry:
      place: client-api::public
  actor: user
- text: Current throttle blocks credential attempt
  kind: product
  entities: []
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
---

# Sign in locked out

## Trigger

The User attempts sign-in while the applicable failure throttle is blocking that request.

## Outcome

Current throttle blocks credential attempt
