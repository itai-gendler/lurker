---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User tries to replace an existing password with an incorrect current-password proof.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Existing password proof fails; replacement refused
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

# Set password wrong current password

## Trigger

The User tries to replace an existing password with an incorrect current-password proof.

## Outcome

Existing password proof fails; replacement refused
