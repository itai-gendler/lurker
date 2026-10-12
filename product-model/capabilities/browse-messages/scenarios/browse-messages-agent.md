---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes browse messages.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Permitted recent/search history query returned, including stored offline history
  kind: product
  entities:
  - entity: message
    effect: reads
    facts:
    - Sender
    - Content
    - Kind
    - Time
    - Self attribution
    - Upstream identity
    - Reply context
    - Highlight information
    - Ignore information
    - Encryption indication
  contexts: *id001
  actor: ai-agent
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/routes/search.ts
- kind: code
  role: implementation
  target: server/routes/activity.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/services/verbs/recentMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/searchMessages.ts
- kind: code
  role: implementation
  target: vue_client/src/lib/historyPaging.ts
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

# Browse messages agent

## Trigger

The AI agent invokes browse messages.

## Outcome

Permitted recent/search history query returned, including stored offline history

The recent_messages and search_messages tools return recorded history while the upstream is offline. Neither call JOINs or reopens a retained closed subject.

## Contract details

recent_messages returns oldest-first bounded contiguous history (default 100, maximum 500), hasOlder and supported countBy sizing; unknown countBy falls back. search_messages returns newest-first matching content (default 50, maximum 100) and hasMore, with structured filter-only searches supported. Server output can be read using the explicit server target even though list_buffers excludes it.
## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
