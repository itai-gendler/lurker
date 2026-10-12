---
appliesTo:
- type: entity
  id: native-push-device
  effect: changes
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  configuredBy: account
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  configuredBy: account
- actors:
  - user
  - administrator
  configuredBy: account
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts#upsertSubscription
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
---

# Native push device changes require the owner or qualified registering account

Only accepted owner re-registration or the both-native installation rebinding exception changes device association and resets health. Attributable configured delivery updates health unattended.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

The Account-configured alternative selects the currently authenticated, unpaused registering caller. A registration may transfer an existing endpoint to that caller only when both stored and incoming transports are native (APNs or FCM). Every other cross-account collision is refused. The route still validates the transport and token/key shape and requires the corresponding configured sender; relay contact remains subject to instance opt-in. The rebinding exception does not admit arbitrary edits of another account’s subscription. Delivery-health updates remain unattended and registration-specific.
