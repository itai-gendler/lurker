---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes browse networks.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: "Authorized account\u2019s network information returned"
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Name
    - Current nick
    - Connection state
  - entity: account
    effect: reads
    facts: []
  contexts: *id001
  actor: ai-agent
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/mcpServer.ts
- kind: code
  role: implementation
  target: server/middleware/apiAuth.ts
- kind: code
  role: implementation
  target: server/services/verbRegistry.ts
- kind: code
  role: implementation
  target: server/services/verbs/listNetworks.ts
---

# Browse networks agent

## Trigger

The AI agent invokes browse networks.

## Outcome

Authorized account’s network information returned

Personal clients receive owned configuration/state. Bouncer control mode exposes its account’s selectable networks; MCP returns its registered projection.

The tool returns the configured names, current nicks and live connected flags. It does not return connection secrets, full preferences or offered presets.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
