---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes change conversation target modes.
  kind: actor
  entities:
  - entity: channel
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: The Product submits the validated MODE batches and returns their request result.
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
  target: server/services/verbs/setChannelModes.ts
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

# Change channel modes agent

## Trigger

The AI agent invokes change channel modes.

## Outcome

Owned mode changes requested through its outbound tool

Supported mode changes are submitted and subsequent upstream results determine observed modes.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.

The tool acknowledgement changes neither the observed Topic, channel Modes nor Current nick and does not rewrite Preferred nick. The corresponding upstream event, if accepted, supplies the observed result.
