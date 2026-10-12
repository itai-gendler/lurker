---
kind: primary
routes:
  agent: MCP agent
steps:
- text: The AI agent invokes send message.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    agent:
      place: mcp
  actor: ai-agent
- text: Supported content submitted through its outbound tool; result follows actual manager outcome
  kind: product
  entities:
  - entity: message
    effect: creates
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
    to: Recorded
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
  target: server/services/verbs/sendMessage.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendAction.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendNotice.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
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

# Send message agent

## Trigger

The AI agent invokes send message.

## Outcome

Supported content submitted through its outbound tool; result follows actual manager outcome

Supported conversation content is submitted through the actual manager contract. A successful acknowledgement is not a recipient-delivery receipt. Supported multiline submission uses negotiated batching or chunks.

## Edge cases

- Message/action/notice and eligible replies use their specific upstream tags. An ineligible reply falls back to supported plain submission rather than fabricating an upstream reference.
- Encrypted channel messages are encrypted for upstream transport but plaintext can be retained server-side. Encryption failure never falls back to sending plaintext.
- Encrypted-channel action/notice refusal can return manager success with an app warning; MCP can therefore return {ok:true} without sending that action or notice.
- The bouncer explicitly refuses encrypted action/notice; self echo, persisted playback and incoming raw ciphertext differ.

## Contract failures

Missing required fields, invalid owned-network selection, unknown tool names and malformed protocol envelopes produce the established registry or JSON-RPC failure. Exceptions are tool results with isError:true; a handler’s {ok:false,error} value is a normal tool result with isError:false. MCP is stateless and returns no subscription stream.
