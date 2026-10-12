---
kind: primary
routes:
  web: Web
  client: Client API
  web-direct-message: Direct Message
  web-network-log: Network Log
steps:
- text: The User asks to show retained history before the current display-clear boundary.
  kind: actor
  entities: []
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
    web-network-log:
      place: web::personal::network-log
  actor: user
- text: When the selected subject is channel, the Product applies the accepted boundary operation only to that subject.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts: &id001
    - Clear boundary
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
    web-network-log:
      place: web::personal::network-log
  actor: user
- text: When the selected subject is direct message, the Product applies the accepted boundary operation only to
    that subject.
  kind: product
  entities:
  - entity: direct-message
    effect: changes
    facts: *id001
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
    web-network-log:
      place: web::personal::network-log
  actor: user
- text: When the selected subject is network log, the Product applies the accepted boundary operation only to that
    subject.
  kind: product
  entities:
  - entity: network-log
    effect: changes
    facts: *id001
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
    web-network-log:
      place: web::personal::network-log
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

# Show earlier messages

## Trigger

The User invokes show earlier messages.

## Outcome

Clear boundary removed

Clear records a display boundary; show-earlier removes it. Both retain underlying history and the independent read pointer.

## Edge cases

- The supported direct-message and network-log operations affect their own Clear boundary. Detached anchored history can bypass the display filter; the Lurker log has no mapped clear operation.

## Decision points

### Selected subject

Which supported subject does this operation address?

- Channel selected → only its own supported facts are affected; the same operation completes.
- Direct Message selected → only its own supported facts are affected; the same operation completes.
- Network Log selected → only its own supported facts are affected; the same operation completes.
