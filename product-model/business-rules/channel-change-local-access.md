---
appliesTo:
- type: entity
  id: channel
  effect: changes
  contexts:
  - place: web::personal
  - place: client-api::personal
  - place: irc-bouncer::personal
  facts:
  - Read boundary
  - Clear boundary
  - Unread counts
  - Retention override
  - Notification override
permits:
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  configuredBy: account
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  configuredBy: account
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
---

# Channel changes require the stated owner or bound entry authority

Only the owner changes the selected subject’s read/clear/retention/notification facts. Local WS read/clear operations keep their actual pause exceptions; HTTP writes retain the active-account guard. A moving bound bouncer timestamp marker advances the shared pointer, while query/nonmoving responses do not.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

Account selects the actual current personal caller or registered bouncer binding. Local WebSocket read/clear operations retain the inspected pause exceptions, while HTTP retention/notification mutations require the current caller unpaused. The binding resolves the selected owned buffer and cannot choose another account’s subject.
