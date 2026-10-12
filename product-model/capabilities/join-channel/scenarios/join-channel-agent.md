---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes join conversation target.
  kind: actor
  entities:
  - entity: channel
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: The Product submits JOIN on the selected live connection and returns the request result.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  contexts: *id001
  actor: ai-agent
- text: Only for the established already-joined path, the Product opens the saved subject and updates its join intent
    and supplied key.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Visibility
    - Autojoin
    - Channel key
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
  target: server/services/verbs/joinChannel.ts
- kind: code
  role: implementation
  target: vue_client/src/components/ChannelListModal.vue
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

# Join channel agent

## Trigger

The AI agent invokes join channel.

## Outcome

Join request accepted; tool success does not prove confirmed membership

The request is sent upstream. Confirmation, or the established already-joined path, sets membership and saved intent; an upstream refusal does not manufacture joined state.

## Edge cases

- A newly established subject receives its supported default view facts. Web pending-join confirmation activates the conversation.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.

## Decision points

### Existing membership

Is the target already joined on the live connection?

- Already joined → the existing subject is opened with autojoin intent and any supplied key, and the request returns success.
- Not already joined → JOIN is submitted and success acknowledges only that submission; the later upstream event determines membership and saved subject changes.
