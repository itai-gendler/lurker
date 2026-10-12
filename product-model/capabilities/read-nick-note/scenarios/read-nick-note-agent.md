---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes read nick note.
  kind: actor
  entities:
  - entity: nick-note
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Owned private note returned
  kind: product
  entities:
  - entity: nick-note
    effect: reads
    facts:
    - Nick
    - Text
    - Updated at
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
  target: server/services/verbs/getNickNote.ts
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

# Read nick note agent

## Trigger

The AI agent invokes read nick note.

## Outcome

Owned private note returned

The tool returns the private text and update time; absence yields an empty note string and null update time.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
