---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User submits an archive that fails validation before replacement begins.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Archive validation fails before replacement mutation
  kind: product
  entities: []
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

# Import data invalid archive

## Trigger

The User submits an archive that fails validation before replacement begins.

## Outcome

Archive validation fails before replacement mutation
