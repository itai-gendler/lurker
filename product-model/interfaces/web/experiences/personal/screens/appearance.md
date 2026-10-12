---
entities:
- entity: account
  shows:
  - Appearance settings
  collects:
  - Appearance settings
- entity: theme
  shows:
  - Name
  - Values
  - Created at
  - Updated at
  collects:
  - Name
  - Values
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/AppearancePane.vue
---

# Appearance

Account Appearance settings and Theme name/values. Collects preferences and saved-theme inputs.
