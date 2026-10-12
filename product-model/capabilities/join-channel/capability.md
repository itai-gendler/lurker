---
availability:
- place: web::personal
- place: client-api::personal
- place: irc-bouncer::personal
- place: mcp
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
---

# Join channel

Join requested; confirmed upstream join establishes membership and intent.

The request is sent upstream. Confirmation, or the established already-joined path, sets membership and saved intent; an upstream refusal does not manufacture joined state.
