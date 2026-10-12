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
  target: server/services/push/relay.ts
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

# Deliver notification

Eligible activity produces a configured provider attempt unattended.

Eligible activity triggers configured delivery attempts. Ordinary messages/actions in DMs, highlights and supported kick events use actual eligibility; notices and self traffic differ.
