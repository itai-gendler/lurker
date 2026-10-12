---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes send raw command.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Permitted raw command submitted through the guarded raw verb
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
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

# Send raw command agent

## Trigger

The AI agent invokes send raw command.

## Outcome

Permitted raw command submitted through the guarded raw verb

The supported raw path sanitizes or validates its command and follows surface-specific forwarding/query routing.

## Edge cases

- MCP rejects multiline input and encrypted-channel raw PRIVMSG. That MCP guard is not asserted for the WS raw path.
- Bound bouncer query replies are routed to their requester; post-registration AUTH is not forwarded as ordinary raw IRC.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
