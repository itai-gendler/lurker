---
kind: primary
routes:
  web: Web
  client: Client API
  web-direct-message: Web direct message
steps:
- text: The User invokes close buffer.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: When the selected subject is a channel, the Product closes its visibility.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Visibility
    - Autojoin
    to: Closed
    from: Open
  contexts: *id001
  actor: user
- kind: product
  actor: user
  text: When the selected subject is a Direct message, the Product closes its visibility.
  entities:
  - entity: direct-message
    effect: changes
    facts:
    - Visibility
    to: Closed
    from: Open
  contexts: *id001
- text: The Product removes the selected conversation’s saved composition and ordering associations.
  kind: product
  entities:
  - entity: draft
    effect: removes
  - entity: pin
    effect: removes
  - entity: favorite-buffer
    effect: removes
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
---

# Close buffer

## Trigger

The User invokes close buffer.

## Outcome

Buffer hidden and associated personal state cleaned; history retained

Closing hides the selected conversation, cleans its draft/pin/favorite associations and lowers join intent. A conditional PART handles possible joined state; retained history is not immediately deleted.

## Edge cases

- The corresponding direct-message operation changes its Visibility to Closed and cleans its personal associations. Later retention/closed collection can remove retained data.
