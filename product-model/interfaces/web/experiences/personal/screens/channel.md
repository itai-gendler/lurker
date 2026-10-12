---
entities:
- entity: channel
  shows:
  - Target
  - Visibility
  - Joined status
  - Autojoin
  - Channel key
  - Topic
  - Members
  - Modes
  - Mode lists
  - Read boundary
  - Clear boundary
  - Unread counts
  - Retention override
  - Notification override
  - Encryption status
  - Events
  collects:
  - Topic
  - Modes
  - Retention override
  - Notification override
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

# Channel

Channel facts, Events, Messages, Reactions and Draft. Collects composition, topic/mode and local-view inputs.
