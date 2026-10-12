---
actors:
- user
references:
- kind: code
  role: implementation
  target: vue_client/src/views/InviteAccept.vue
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/db/invites.ts
---

# Invitation to chat

## Goal

Accept an invitation and arrive in usable personal chat.

## Success criterion

The invitation is consumed, account access is issued, and the carried person can browse their buffers.
