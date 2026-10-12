---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent submits a WHOIS lookup.
  kind: actor
  entities: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: The Product submits WHOIS and returns acknowledgement plus the exact retained-output target for a separate
    later query.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  - entity: network-log
    effect: reads
    facts: []
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
  target: server/services/verbs/whois.ts
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

# Look up user agent

## Trigger

The AI agent invokes look up user.

## Outcome

WHOIS request accepted through its outbound tool; subsequent result requires a separate read

WHOIS requests observation. Web/profile results can be partial; MCP acknowledges the outbound request and later output requires a separate history read.

## Edge cases

- MCP has no asynchronous stream and does not automatically perform that later read.

## Contract details

The tool sends WHOIS through the writable connection and returns {ok:true,serverBuffer,note}. The serverBuffer is the exact target for a later recent_messages call. It does not return profile fields or automatically perform that later read.
## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
