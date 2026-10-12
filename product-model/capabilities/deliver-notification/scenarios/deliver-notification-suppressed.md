---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: Recorded activity reaches the notification eligibility check.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  unattended: true
- text: Eligibility/presence/settings/policy suppress provider attempt unattended
  kind: product
  entities:
  - entity: account
    effect: reads
    facts:
    - Notification settings
    - Away settings
  contexts: *id001
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
---

# Deliver notification suppressed

## Trigger

The Product considers activity for notification while presence, preferences or instance policy suppress delivery.

## Outcome

Eligibility/presence/settings/policy suppress provider attempt unattended
