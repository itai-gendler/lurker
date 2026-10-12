---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User invokes send message.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: Supported content submitted; recording/echo follows the actual send contract
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
  actor: user
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
---

# Send message

## Trigger

The User invokes send message.

## Outcome

Supported content submitted; recording/echo follows the actual send contract

Supported conversation content is submitted through the actual manager contract. A successful acknowledgement is not a recipient-delivery receipt. Supported multiline submission uses negotiated batching or chunks.

## Edge cases

- Message/action/notice and eligible replies use their specific upstream tags. An ineligible reply falls back to supported plain submission rather than fabricating an upstream reference.
- Encrypted channel messages are encrypted for upstream transport but plaintext can be retained server-side. Encryption failure never falls back to sending plaintext.
- Encrypted-channel action/notice refusal can return manager success with an app warning; MCP can therefore return {ok:true} without sending that action or notice.
- The bouncer explicitly refuses encrypted action/notice; self echo, persisted playback and incoming raw ciphertext differ.
