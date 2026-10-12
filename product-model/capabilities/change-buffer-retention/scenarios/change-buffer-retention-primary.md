---
kind: primary
routes:
  web: Web
  client: Client API
  web-direct-message: Direct Message
steps:
- text: The User invokes change buffer retention.
  kind: actor
  entities: []
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: When the selected subject is channel, the Product applies the accepted boundary operation only to that subject.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts: &id001
    - Retention override
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
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
  target: server/routes/retention.ts
- kind: code
  role: implementation
  target: server/services/retentionLimits.ts
---

# Change buffer retention

## Trigger

The User invokes change buffer retention.

## Outcome

Override saved or returned to inheritance

The selected channel or direct-message override changes or returns to inheritance, under effective account/instance ceilings.

## Decision points

### Selected subject

Which supported subject does this operation address?

- Channel selected → only its own supported facts are affected; the same operation completes.
- Direct Message selected → only its own supported facts are affected; the same operation completes.
