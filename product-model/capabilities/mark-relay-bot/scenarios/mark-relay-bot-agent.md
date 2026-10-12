---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes mark relay bot.
  kind: actor
  entities:
  - entity: relay-bot
    effect: reads
    facts: []
    as: existing-relay-bot
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: For a previously unmarked nick, the Product records the relay-bot nick, envelope template and creation time.
  kind: product
  entities:
  - entity: relay-bot
    effect: creates
    facts:
    - Nick
    - Envelope template
    - Created at
    as: new-relay-bot
  contexts: *id001
  actor: ai-agent
- text: For an existing relay-bot nick, the Product replaces its trimmed envelope template.
  kind: product
  entities:
  - entity: relay-bot
    effect: changes
    facts:
    - Envelope template
    as: existing-relay-bot
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
  target: server/services/verbs/setRelayBot.ts
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

# Mark relay bot agent

## Trigger

The AI agent invokes mark relay bot.

## Outcome

Owned relay attribution mark saved

The network/nick envelope mark is saved or replaced. Supported templates unwrap display attribution with bounded nesting while retaining original content.

## Edge cases

- The mark does not prove the embedded sender’s identity. Invalid templates do not produce invented attribution.

## Contract details

The tool saves/replaces the scoped mark, caps the template at 512 characters and returns canonical stored nick casing with the saved mark/pattern; account WebSocket clients receive the same update.
## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.

## Decision points

### Existing selected record

Does the selected record already exist?

- Absent record → create it with its supported initial/default values.
- Existing record → update that same selected record; no independent duplicate is created.
