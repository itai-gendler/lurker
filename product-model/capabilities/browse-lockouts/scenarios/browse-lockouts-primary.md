---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes browse lockouts.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::lockouts
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Current blocked addresses and login policy returned
  kind: product
  entities:
  - entity: instance-settings
    effect: reads
    facts:
    - Blocked sign-ins
    - Login policy
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/middleware/rateLimit.ts
---

# Browse lockouts

## Trigger

The Administrator invokes browse lockouts.

## Outcome

Current blocked addresses and login policy returned
