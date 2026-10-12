---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes edit nick note.
  kind: actor
  entities:
  - entity: nick-note
    effect: reads
    facts: []
    as: existing-nick-note
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: When no scoped note exists, the Product saves trimmed private text and its update time.
  kind: product
  entities:
  - entity: nick-note
    effect: creates
    facts:
    - Nick
    - Text
    - Updated at
    as: new-nick-note
  contexts: *id001
  actor: ai-agent
- text: For the existing scoped note, the Product replaces private text and update time and synchronizes the result.
  kind: product
  entities:
  - entity: nick-note
    effect: changes
    facts:
    - Text
    - Updated at
    as: existing-nick-note
  contexts:
    agent:
      place: mcp
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
  target: server/services/verbs/setNickNote.ts
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

# Edit nick note agent

## Trigger

The AI agent invokes edit nick note.

## Outcome

Owned private note saved/changed

A network-scoped nick note is saved, trimmed and synchronized. Absent notes are created; text is limited to 4096 characters.

The tool trims the scoped nick, caps text at 4096 characters, saves/replaces it, and fans out the result to the account’s WebSocket clients.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.

## Decision points

### Existing selected record

Does the selected record already exist?

- Absent record → create it with its supported initial/default values.
- Existing record → update that same selected record; no independent duplicate is created.
