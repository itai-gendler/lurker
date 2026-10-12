---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes reconnect configured upstream.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Host policy checked before force-restart; replacement dial requested
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
  target: server/services/verbs/connectNetwork.ts
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

# Reconnect network agent

## Trigger

The AI agent invokes reconnect network.

## Outcome

Host policy checked before force-restart; replacement dial requested

The host/proxy policy and account state are checked before requesting a dial. Reconnect replaces the prior connection; MCP force:true is its reconnect path.

## Edge cases

- Registration and later failure arrive asynchronously; request acceptance is not confirmed connection success.

## Contract details

force:true checks host policy before replacing a working connection, then returns start acceptance. Later registration/failure is separate.
## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
