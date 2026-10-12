---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes change topic.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: The Product submits TOPIC on the selected live connection and returns the request result.
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
  target: server/services/verbs/setTopic.ts
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

# Change topic agent

## Trigger

The AI agent invokes change topic.

## Outcome

Owned topic change requested through its outbound tool

The requested topic is submitted; the upstream governs acceptance and observed topic results.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.

The tool acknowledgement changes neither the observed Topic, channel Modes nor Current nick and does not rewrite Preferred nick. The corresponding upstream event, if accepted, supplies the observed result.
