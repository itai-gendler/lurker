---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes disconnect configured upstream.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Owned connection stopped; retained data remains
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Connection state
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
  target: server/services/verbs/disconnectNetwork.ts
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

# Disconnect network agent

## Trigger

The AI agent invokes disconnect network.

## Outcome

Owned connection stopped; retained data remains

Stopping the upstream retains saved configuration and history.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
