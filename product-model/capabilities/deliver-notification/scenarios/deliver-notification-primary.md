---
kind: primary
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
- text: Eligible activity produces a configured provider attempt unattended
  kind: product
  entities:
  - entity: message
    effect: reads
    facts:
    - Sender
    - Content
    - Kind
    - Highlight information
    - Ignore information
    - Self attribution
  - entity: account
    effect: reads
    facts:
    - Notification settings
    - Away settings
  - entity: web-push-subscription
    effect: changes
    facts:
    - Last seen at
    - Delivery health
    - Enabled
  - entity: native-push-device
    effect: changes
    facts:
    - Last seen at
    - Delivery health
    - Enabled
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

## Trigger

Recorded activity reaches the notification eligibility check.

## Outcome

Eligible activity produces a configured provider attempt unattended

Eligible activity triggers configured delivery attempts. Ordinary messages/actions in DMs, highlights and supported kick events use actual eligibility; notices and self traffic differ.

## Edge cases

- Visible WebSocket presence suppresses phone push, independently of counted IRC presence. Quiet time, mute, away and per-channel preferences can suppress delivery.
- Relay registration/delivery requires opt-in. Permanent 404/410 failures remove registrations; counted failures can disable at the established threshold; transient failures are classified separately.
