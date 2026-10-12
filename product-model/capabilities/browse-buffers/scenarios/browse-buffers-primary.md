---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes browse buffers.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Surface-specific enumeration of owned conversation subjects
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Target
    - Visibility
    - Unread counts
  - entity: direct-message
    effect: reads
    facts:
    - Target
    - Visibility
    - Unread counts
  - entity: network
    effect: reads
    facts:
    - Name
    - Current nick
    - Connection state
  contexts: *id001
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
  target: server/services/verbs/listBuffers.ts
---

# Browse buffers

## Trigger

The User invokes browse buffers.

## Outcome

Surface-specific enumeration of owned conversation subjects

Web/API hydration enumerates owned subjects. MCP aggregates message-bearing channel/DM targets, excluding server/system/DCC subjects and without filtering closed status. Bouncer control/attachment contracts differ.
