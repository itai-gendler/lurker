---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes clear lockouts.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::lockouts
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Current blocked entries lifted
  kind: product
  entities:
  - entity: instance-settings
    effect: changes
    facts:
    - Blocked sign-ins
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

# Clear lockouts

## Trigger

The Administrator invokes clear lockouts.

## Outcome

Current blocked entries lifted

Currently blocked entries are lifted; subthreshold failure budgets are retained.
