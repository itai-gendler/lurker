---
appliesTo:
- type: entity
  id: message
- type: entity
  id: bookmark
- type: entity
  id: account
- type: entity
  id: channel
- type: entity
  id: direct-message
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Retention effective limits

Effective account/buffer limits obey instance ceilings. Zero means unbounded only where no effective ceiling constrains it. Bookmarks remain protected; reply context is bounded, including the implemented cap relative to the ceiling. Relevant import and in-flight export work defer pruning; failures follow the established bounded retry and warning behavior.
