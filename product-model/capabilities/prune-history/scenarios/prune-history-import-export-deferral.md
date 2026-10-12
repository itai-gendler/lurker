---
kind: exception
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
- text: Unattended pruning deferred during the relevant import/export work
  kind: product
  entities:
  - entity: data-export
    effect: reads
    facts:
    - Progress
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

# Prune history import export deferral

## Trigger

The Product considers pruning while the relevant import or export work is in progress.

## Outcome

Unattended pruning deferred during the relevant import/export work
