---
appliesTo:
- type: entity
  id: web-push-subscription
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

# Web Push subscription changes require the owner or qualified registering account

Only the owner’s accepted heartbeat/re-registration changes its endpoint association, except the both-WebPush relay-device rebinding exception assigns the signing-in account. Delivery attempts update health unattended under eligibility/opt-in and provider classification.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

The Account-configured alternative selects the currently authenticated, unpaused registering caller. A registration may transfer an existing endpoint to that caller only when both stored and incoming transports are Web Push and the endpoint identifies a relay device. Every other cross-account collision is refused. The route still validates the transport and token/key shape and requires the corresponding configured sender; relay contact remains subject to instance opt-in. The rebinding exception does not admit arbitrary edits of another account’s subscription. Delivery-health updates remain unattended and registration-specific.
