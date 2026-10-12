---
appliesTo:
- type: entity
  id: account
- type: entity
  id: session
- type: entity
  id: passkey
- type: entity
  id: api-token
- type: entity
  id: authorized-app
- type: entity
  id: irc-client
- type: entity
  id: web-push-subscription
- type: entity
  id: native-push-device
references:
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/webauthnCredentials.ts
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
---

# Recovery replaces access

A valid 24-hour, single-use recovery link replaces the old password/passkeys, deletes ordinary sessions, revokes API-token and OAuth access, drops associated push registrations and closes evidenced live WebSocket/bouncer access. Fresh ordinary access is issued only after the successful replacement. No mail delivery is implied.
