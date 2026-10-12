---
appliesTo:
- type: entity
  id: web-push-subscription
- type: entity
  id: native-push-device
- type: entity
  id: instance-settings
- type: entity
  id: account
references:
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/routes/config.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
---

# Push policy and health

Actual eligibility, self filtering, visible-WebSocket suppression, quiet time, channel/account preferences and relay opt-in govern provider attempts. Ordinary browser cross-owner endpoints refuse rebind; both-native and both-WebPush relay-device exceptions may rebind. Native removal matches owner+endpoint without a transport predicate. Successful re-registration/delivery resets health; permanent 404/410 cleanup, counted failure disabling and transient classifications remain distinct. Explicit administrative relay checks can contact the service while delivery is disabled.
