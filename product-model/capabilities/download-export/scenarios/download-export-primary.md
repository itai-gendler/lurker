---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes download export.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Ready owned artifact downloaded
  kind: product
  entities:
  - entity: data-export
    effect: reads
    facts:
    - Artifact
    - Progress
    - Expires at
  contexts: *id001
  actor: user
- text: The Product records the completed download time.
  kind: product
  entities:
  - entity: data-export
    effect: changes
    facts:
    - Downloaded at
  contexts:
    web:
      place: web::personal::data
    client:
      place: client-api::personal
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

# Download export

## Trigger

The User invokes download export.

## Outcome

Ready owned artifact downloaded

Only a ready, present owned artifact is returned, with supported range download; readiness conflicts and missing/expired artifacts fail distinctly.
