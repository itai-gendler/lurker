---
kind: validation
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User presents an unknown, expired or already-consumed invitation.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::invite
    client-entry:
      place: client-api::public
  actor: user
- text: Unknown, expired or consumed invitation refused
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
  target: server/db/invites.ts
---

# Accept invite unusable invite

## Trigger

The User presents an unknown, expired or already-consumed invitation.

## Outcome

Unknown, expired or consumed invitation refused
