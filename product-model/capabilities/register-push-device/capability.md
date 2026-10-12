---
availability:
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/services/pushService.ts
- kind: code
  role: implementation
  target: server/services/push/index.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Register push device

Valid supported native installation registered.

A validated installation token for a configured supported native sender is registered or rebound under the stored/incoming native transport checks.
