---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes browse buffers.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Message-bearing conversation targets returned by the actual query
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Target
  - entity: direct-message
    effect: reads
    facts:
    - Target
  - entity: network
    effect: reads
    facts: []
  - entity: message
    effect: reads
    facts:
    - Time
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
  target: server/services/verbs/listBuffers.ts
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

# Browse buffers agent

## Trigger

The AI agent invokes browse buffers.

## Outcome

Message-bearing conversation targets returned by the actual query

Web/API hydration enumerates owned subjects. MCP aggregates message-bearing channel/DM targets, excluding server/system/DCC subjects and without filtering closed status. Bouncer control/attachment contracts differ.

The tool returns network association, target, channel/DM kind and last recorded time, ordered by freshness. It does not return visibility or unread counts and does not filter out closed subjects.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
