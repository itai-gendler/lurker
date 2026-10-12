---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes read topic.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Owned current/last-known topic returned through its observation tool
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Topic
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
  target: server/services/verbs/getTopic.ts
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

# Read topic agent

## Trigger

The AI agent invokes read topic.

## Outcome

Owned current/last-known topic returned through its observation tool

Current or last-known topic is returned through the MCP observation tool. A bouncer topic query follows upstream IRC.

The tool reads current/last-known topic from the retained connection object through its observation tool. It can return null for unset topic, not-connected for no object, or not-in-channel for no observed subject; it does not require a fresh upstream query.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
