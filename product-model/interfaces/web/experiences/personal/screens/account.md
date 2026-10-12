---
entities:
- entity: account
  shows:
  - Username
  - Sign-in methods
  collects:
  - Sign-in methods
- entity: passkey
  shows:
  - Label
  - Device information
  - Created at
  - Last used at
  collects:
  - Label
  - Registration
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/AccountPane.vue
entryPoints:
- web: /settings/account
---

# Account

Own username/sign-in methods and Passkey label/device/timestamps. Collects sign-in method changes.
