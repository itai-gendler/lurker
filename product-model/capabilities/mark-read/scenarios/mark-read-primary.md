---
kind: primary
routes:
  web: Web
  client: Client API
  web-direct-message: Direct Message
  web-network-log: Network Log
  web-lurker-log: Lurker Log
steps:
- text: The User invokes mark read.
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
    web-lurker-log:
      place: web::personal::lurker-log
  actor: user
- text: When the selected subject is channel, the Product applies the accepted boundary operation only to that subject.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts: &id001
    - Read boundary
    - Unread counts
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
    web-network-log:
      place: web::personal::network-log
    web-lurker-log:
      place: web::personal::lurker-log
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
    web-lurker-log:
      place: web::personal::lurker-log
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
    web-lurker-log:
      place: web::personal::lurker-log
  actor: user
- text: When the selected subject is lurker log, the Product applies the accepted boundary operation only to that
    subject.
  kind: product
  entities:
  - entity: lurker-log
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
    web-lurker-log:
      place: web::personal::lurker-log
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
  target: server/db/bufferReads.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Mark read

## Trigger

The User invokes mark read.

## Outcome

Shared read pointer advances monotonically

The accepted shared read pointer advances with MAX semantics. WS accepts a positive finite ID without checking integer, submitted-buffer membership or tail bounds.

## Edge cases

- Web activation, hydration and active arrivals mark loaded tails, not viewport reading. A detached jump may first mark the known live tail.
- Direct-message and network-log markers use their own read/count facts; the networkless Lurker log uses its own sequence. Bouncer markers exclude server/system/DCC.
- Bouncer MARKREAD resolves timestamps to retained history and moving updates fan out; queries and nonadvancing replies remain local to the requester.

## Decision points

### Selected subject

Which supported subject does this operation address?

- Channel selected → only its own supported facts are affected; the same operation completes.
- Direct Message selected → only its own supported facts are affected; the same operation completes.
- Network Log selected → only its own supported facts are affected; the same operation completes.
- Lurker Log selected → only its own supported facts are affected; the same operation completes.
