---
entities:
- entity: network
  shows:
  - Listed channels
  - Directory progress
references:
- kind: code
  role: implementation
  target: vue_client/src/components/ChannelListModal.vue
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Channel list

Network Listed channels and Directory progress. Collects filtering/sorting/join selection; exposes refresh.
