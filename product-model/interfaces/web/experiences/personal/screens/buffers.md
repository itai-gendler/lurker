---
entities:
- entity: network
  shows:
  - Name
  - Current nick
  - Connection state
  - Position
- entity: channel
  shows:
  - Target
  - Visibility
  - Unread counts
- entity: direct-message
  shows:
  - Target
  - Visibility
  - Unread counts
- entity: pin
  shows:
  - Position
  collects:
  - Position
- entity: favorite-buffer
  shows:
  - Position
  collects:
  - Position
references:
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
entryPoints:
- web: /
---

# Buffers

Owned Network name/current nick/connection state; conversation target/visibility/unread counts; pin/favorite positions.
