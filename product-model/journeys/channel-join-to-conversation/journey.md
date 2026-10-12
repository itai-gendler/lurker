---
actors:
- user
references:
- kind: code
  role: implementation
  target: vue_client/src/components/ChannelListModal.vue
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
---

# Channel join to conversation

## Goal

Join a channel and arrive in its usable conversation.

## Success criterion

Upstream join confirmation activates the conversation, where the carried person can browse its retained content.
