---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes sign out.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Presented credential removed; browser account state reset
  kind: product
  entities:
  - entity: session
    effect: removes
    from: Issued
  - entity: account
    effect: reads
    facts: []
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

# Sign out

## Trigger

The User invokes sign out.

## Outcome

Presented credential removed; browser account state reset

Only the presented ordinary session is removed. The web client resets its account state. Already-authenticated sockets are not globally terminated by this ordinary logout.

## Edge cases

- A password change does not prove global ordinary-session or socket revocation.
