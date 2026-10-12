---
kind: validation
routes:
  agent: MCP agent
steps:
- text: The AI agent submits a raw PRIVMSG naming an encryption-enabled conversation target.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: "AI agent\u2019s raw PRIVMSG to encrypted channel refused by MCP raw guard"
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts: []
  contexts: *id001
  actor: ai-agent
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
  target: server/services/verbs/sendRaw.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
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

# Send raw command mcp encrypted privmsg refused

## Trigger

The AI agent submits a raw PRIVMSG naming an encryption-enabled channel.

## Outcome

AI agent’s raw PRIVMSG to encrypted channel refused by MCP raw guard
