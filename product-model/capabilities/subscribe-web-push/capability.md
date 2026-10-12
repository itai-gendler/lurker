---
availability:
- place: web::personal
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
domain: notifications
---

# Subscribe web push

Web Push endpoint/keys registered under endpoint ownership rules.

Validated endpoint and delivery keys register or refresh the account’s Web Push delivery association.
