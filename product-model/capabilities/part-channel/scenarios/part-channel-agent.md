---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes part conversation target.
  kind: actor
  entities:
  - entity: channel
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: PART requested and autojoin intent lowered
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Autojoin
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
  target: server/services/verbs/partChannel.ts
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

# Part channel agent

## Trigger

The AI agent invokes part channel.

## Outcome

PART requested and autojoin intent lowered

PART lowers join intent while retaining the buffer/history. The bouncer does not establish the comment’s second-PART/Close equivalence.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.

The immediate kept effect is lowering autojoin on an existing subject. Joined status changes only when the upstream membership event is observed; no missing buffer is created by lowering intent.
