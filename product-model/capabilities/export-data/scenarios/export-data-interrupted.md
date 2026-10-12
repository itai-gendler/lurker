---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The established presence or startup condition is observed.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  unattended: true
- text: Startup recovery moves an interrupted running job to Failed rather than leaving perpetual progress.
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

# Export data interrupted

## Trigger

The Product starts with a previously interrupted export job.

## Outcome

Startup recovery moves an interrupted running job to Failed rather than leaving perpetual progress.
