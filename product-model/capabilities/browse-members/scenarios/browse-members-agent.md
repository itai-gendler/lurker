---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes browse members.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Owned observed membership returned through its observation tool
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Members
  - entity: irc-user
    effect: reads
    facts:
    - Nick
    - Membership status
    - Presence
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
  target: server/services/verbs/listMembers.ts
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

# Browse members agent

## Trigger

The AI agent invokes browse members.

## Outcome

Owned observed membership returned through its observation tool

Observed membership is returned; MCP sorts results and reports truncation/total with its default 200 and maximum 1000 result limit.

The observed member projection contains nick, prefix modes and away state, sorted by nick with default 200/maximum 1000. count remains the total and truncated describes the returned page. A retained connection object can provide last-known membership during reconnect; absence of the object or subject returns not-connected/not-in-channel.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
