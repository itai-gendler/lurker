---
availability:
- place: web::personal
- place: client-api::personal
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
  target: server/routes/retention.ts
- kind: code
  role: implementation
  target: server/services/retentionLimits.ts
---

# Change buffer retention

Override saved or returned to inheritance.

The selected channel or direct-message override changes or returns to inheritance, under effective account/instance ceilings.
