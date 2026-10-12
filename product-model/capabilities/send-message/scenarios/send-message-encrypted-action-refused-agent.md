---
kind: exception
routes:
  agent: MCP agent
steps:
- text: The AI agent submits an action to an encryption-enabled conversation target.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: The manager sends no action, yet the tool can return {ok:true}. Its ephemeral app warning is not delivered
    through an MCP subscription.
  kind: product
  entities: []
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
  target: server/services/verbs/sendMessage.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendAction.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendNotice.ts
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

# Send message encrypted action refused agent

## Trigger

The AI agent submits an action to an encryption-enabled channel.

## Outcome

The manager sends no action, yet the tool can return {ok:true}. Its ephemeral app warning is not delivered through an MCP subscription.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
