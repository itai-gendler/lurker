---
appliesTo:
- type: entity
  id: account
  effect: creates
permits:
- actors:
  - user
  - administrator
  configuredBy: instance-settings
- actors:
  - user
  - administrator
  configuredBy: invite
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
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/db/sessions.ts#findSession
---

# Only valid first setup or invitation entry creates its resulting Account

The Instance-settings-configured alternative admits first setup only while no user exists. Valid unique username and supported password input create the first Administrator. Passkey setup options instead create the provisional Administrator and bind a setup-purpose challenge to that account; verification retains its separate credential-count race guard and can fail without an atomic setup-completion guarantee.

The Invite-configured alternative selects the exact invitation presented for redemption, not any available invitation. It must currently exist, be unexpired and be unconsumed. Username and selected password/passkey input validate. Passkey verification uses the signed invitation-purpose challenge with the same invitation and provisional account, rechecks validity, and consumes atomically so only one parallel redemption wins. Invitation entry creates the personal User account, not a caller-selected administrative role.
