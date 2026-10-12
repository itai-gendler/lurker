---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  agent: MCP agent
steps:
- text: The retention maintenance schedule examines eligible retained data.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
    agent:
      place: mcp
  unattended: true
- text: Eligible retained history removed unattended
  kind: product
  entities:
  - entity: message
    effect: removes
    from: Recorded
  contexts: *id001
references:
- kind: code
  role: implementation
  target: server/services/retentionSweeper.ts
- kind: code
  role: implementation
  target: server/services/retentionLimits.ts
- kind: code
  role: implementation
  target: server/db/retention.ts
- kind: code
  role: implementation
  target: server/services/mcpServer.ts
- kind: code
  role: implementation
  target: server/middleware/apiAuth.ts
- kind: code
  role: implementation
  target: server/services/verbRegistry.ts
---

# Prune history

## Trigger

The retention maintenance schedule examines eligible retained data.

## Outcome

Eligible retained history removed unattended

Effective account/buffer retention under instance ceilings removes eligible history unattended. Bookmarks and bounded additional reply-thread context remain protected.

## Edge cases

- Relevant in-flight import/export work defers pruning. Retained reply context is bounded rather than a guarantee to retain an entire thread forever.
