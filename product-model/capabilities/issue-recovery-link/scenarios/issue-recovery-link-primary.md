---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes issue recovery link.
  kind: actor
  entities:
  - entity: recovery-link
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: New single-use recovery link issued
  kind: product
  entities:
  - entity: recovery-link
    effect: creates
    facts:
    - Expires at
    - Validity
    to: Issued
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
  target: server/db/accountRecovery.ts
---

# Issue recovery link

## Trigger

The Administrator invokes issue recovery link.

## Outcome

New single-use recovery link issued

Standalone issuance creates a 24-hour recovery proof, supersedes earlier access links and returns the URL for administrator hand-off.
