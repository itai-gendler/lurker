---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User requests import while the member identity already has a configured upstream.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Existing network makes account ineligible
  kind: product
  entities:
  - entity: account
    effect: reads
    facts: []
  - entity: network
    effect: reads
    facts: []
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

# Import data nonempty account

## Trigger

The User requests import while the account already has a network.

## Outcome

Existing network makes account ineligible
