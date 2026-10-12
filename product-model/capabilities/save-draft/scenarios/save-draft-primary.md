---
kind: primary
routes:
  web: Web
  client: Client API
  web-direct-message: Web direct message
steps:
- text: The User invokes save draft.
  kind: actor
  entities:
  - entity: draft
    as: existing-draft
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: For previously absent composition, the Product retains the submitted text and supported reply reference.
  kind: product
  entities:
  - entity: draft
    effect: creates
    facts:
    - Text
    - Reply reference
    - Updated at
    as: new-draft
  contexts: *id001
  actor: user
- text: For existing composition, the Product replaces the selected saved text and reply reference under the last-write
    contract.
  kind: product
  entities:
  - entity: draft
    effect: changes
    as: existing-draft
    facts:
    - Text
    - Reply reference
    - Updated at
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/routes/drafts.ts
- kind: code
  role: implementation
  target: server/db/drafts.ts
---

# Save draft

## Trigger

The User invokes save draft.

## Outcome

Last-write draft synchronized

Last-write composition text and optional valid owned reply reference are synchronized to other clients. An existing draft is replaced; empty text without reply clears it.

## Edge cases

- An invalid reply is dropped while supported text remains. Legacy omitted reply fields keep their compatibility behavior. Local WS save/clear and HTTP flush have different pause guards.
