---
actors:
- user
references:
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/DataPane.vue
- kind: code
  role: implementation
  target: server/routes/exports.ts
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
---

# Import to chat

## Goal

Import an eligible archive and arrive in usable restored chat.

## Success criterion

Replacement succeeds, web client state is reset, and the carried person can browse restored buffers.
