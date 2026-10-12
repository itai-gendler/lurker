---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User requests an export artifact that is not ready, missing or expired.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Not-ready, missing or expired artifact refused
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

# Download export unavailable

## Trigger

The User requests an export artifact that is not ready, missing or expired.

## Outcome

Not-ready, missing or expired artifact refused
