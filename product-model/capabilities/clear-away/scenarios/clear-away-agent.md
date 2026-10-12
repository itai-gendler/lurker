---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes clear away.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Applicable owned away state cleared
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Away state
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
  target: server/services/verbs/setAway.ts
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

# Clear away agent

## Trigger

The AI agent invokes clear away.

## Outcome

Applicable owned away state cleared

Manual away/back uses the applicable network scope. Automatic away is separately triggered by counted presence and never overwrites manual away.

Empty/omitted reason clears the applicable owned network scope and reports away:false; this does not indiscriminately clear another account’s away state.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
