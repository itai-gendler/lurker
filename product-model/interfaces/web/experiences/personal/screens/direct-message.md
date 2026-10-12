---
entities:
- entity: direct-message
  shows:
  - Target
  - Visibility
  - Peer presence
  - Read boundary
  - Clear boundary
  - Unread counts
  - Retention override
  - Events
  collects:
  - Retention override
- entity: message
  shows:
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
  collects:
  - Content
  - Kind
  - Reply context
- entity: reaction
  shows:
  - Value
  - Reacting identity
  - Self attribution
  - Reacted at
  - Removed at
- entity: draft
  shows:
  - Text
  - Reply reference
  - Updated at
  collects:
  - Text
  - Reply reference
references:
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Direct message

Direct-message facts, Events, Messages, Reactions and Draft. Collects composition.
