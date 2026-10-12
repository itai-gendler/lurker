---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes browse mode list.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Live owned list-mode query returned through its outbound tool
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Mode lists
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
  target: server/services/verbs/getModeList.ts
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

# Browse mode list agent

## Trigger

The AI agent invokes browse mode list.

## Outcome

Live owned list-mode query returned through its outbound tool

A live supported list-mode query returns its result, refusal or timeout. The query sends upstream traffic.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
