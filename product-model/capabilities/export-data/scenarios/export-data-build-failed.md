---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User requests export whose background artifact construction fails.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: The background job reaches Failed and records its error without claiming a ready artifact.
  kind: product
  entities:
  - entity: data-export
    effect: changes
    facts:
    - Progress
    - Error
    to: Failed
    from: Running
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

# Export data build failed

## Trigger

The User requests export whose background artifact construction fails.

## Outcome

The background job reaches Failed and records its error without claiming a ready artifact.
