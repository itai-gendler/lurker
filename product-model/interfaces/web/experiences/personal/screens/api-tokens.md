---
entities:
- entity: api-token
  shows:
  - Name
  - Scope
  - Created at
  - Last used at
  - Revocation
  collects:
  - Name
  - Scope
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/ApiTokensPane.vue
---

# API tokens

Token name/scope/timestamps/revocation. Collects creation/revocation; raw token is revealed only on creation.
