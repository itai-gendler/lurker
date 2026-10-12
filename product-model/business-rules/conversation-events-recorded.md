---
appliesTo:
- type: entity
  id: channel
- type: entity
  id: direct-message
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Conversation events recorded

Established upstream conversation events are recorded and presented as the Channel/Direct message Events facts, without independent event-entry identities.
