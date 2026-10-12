---
kind: validation
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The Administrator requests first setup after setup is complete or with invalid member identity input.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::login
    client-entry:
      place: client-api::public
  actor: administrator
- text: Completed setup or invalid account input refuses setup
  kind: product
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts: *id001
  actor: administrator
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

# Setup lurker invalid setup

## Trigger

The Administrator requests first setup after setup is complete or with invalid account input.

## Outcome

Completed setup or invalid account input refuses setup
