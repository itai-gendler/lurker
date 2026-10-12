---
appliesTo:
- type: entity
  id: web-push-subscription
  effect: removes
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
- actors:
  - user
  - administrator
  configuredBy: recovery-link
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
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
---

# Web Push subscription removal requires the stated owner or bound entry authority

HTTP Owner; ordinary browser cross-owner collision refused; both-WebPush relay-device rebind exception; relay policy gate; owned heartbeat/removal and unattended health.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

The Recovery-link-configured exception requires the exact still-live presented proof and successful supported credential replacement for its bound account. It removes that recovered account’s prior registrations regardless of the target’s Pause status. An ordinary authenticated deregistration retains the active-owner guard; proof spending does not expose a general cross-account deletion endpoint.

The Account-configured ordinary removal grant selects the actual authenticated, unpaused caller and only its exact endpoint match. DELETE /devices and DELETE /subscriptions share that lookup and do not require the row’s transport to match the route’s name; a different owner’s row is unchanged. The qualified recovery and unattended provider/credential cleanup alternatives retain their independent boundaries.

The same authenticated active owner may also replace its endpoint’s stored transport class through an accepted registration. The prior class-specific subject is replaced by the incoming class’s subject under upsertSubscription’s actual same-owner branch; it is not a general cross-account rebinding exception or a provider-byte deletion. The incoming route still applies its sender/relay and field prerequisites.
