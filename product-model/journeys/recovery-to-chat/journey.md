---
actors:
- user
references:
- kind: code
  role: implementation
  target: vue_client/src/views/AccountRecovery.vue
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
  target: server/db/accountRecovery.ts
---

# Recovery to chat

## Goal

Replace compromised sign-in access and arrive in usable personal chat.

## Success criterion

The recovery replacement completes, fresh access is issued, and the carried person can browse their buffers.
