---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User requests export while an in-flight job already exists for the member identity.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Existing in-flight job reused rather than duplicated
  kind: product
  entities:
  - entity: data-export
    effect: reads
    facts:
    - Requested contents
    - Progress
    - Counts
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/exports.ts
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/DataPane.vue
---

# Export data existing job

## Trigger

The User requests export while an in-flight job already exists for the account.

## Outcome

Existing in-flight job reused rather than duplicated
