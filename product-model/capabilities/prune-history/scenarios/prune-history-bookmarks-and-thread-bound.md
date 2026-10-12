---
kind: path
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
- text: Unattended pruning preserves bookmarks and bounded reply context
  kind: product
  entities:
  - entity: message
    effect: removes
    from: Recorded
  - entity: bookmark
    effect: reads
    facts: []
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

# Prune history bookmarks and thread bound

## Trigger

The Product reaches the retention boundary for history containing bookmarks and reply context.

## Outcome

Unattended pruning preserves bookmarks and bounded reply context
