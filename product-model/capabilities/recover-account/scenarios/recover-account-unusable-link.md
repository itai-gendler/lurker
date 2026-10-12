---
kind: validation
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User presents an unknown, expired, spent or superseded recovery proof.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::account-recovery
    client-entry:
      place: client-api::public
  actor: user
- text: Unknown, expired, spent or superseded link refused
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
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
---

# Recover account unusable link

## Trigger

The User presents an unknown, expired, spent or superseded recovery link.

## Outcome

Unknown, expired, spent or superseded link refused
