---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes connect configured upstream.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Permitted start request accepted; upstream registration not guaranteed
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

# Connect network agent

## Trigger

The AI agent invokes connect network.

## Outcome

Permitted start request accepted; upstream registration not guaranteed

The host/proxy policy and account state are checked before requesting a dial. Reconnect replaces the prior connection; MCP force:true is its reconnect path.

## Edge cases

- Registration and later failure arrive asynchronously; request acceptance is not confirmed connection success.

## Contract details

The tool returns {ok:true} only for an accepted start object. An already-connected nonforce request is idempotent. Disallowed host returns locked-down before a force restart; failure to start returns failed.
## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
