---
entities:
- entity: instance-settings
  shows:
  - Versions
  - Edition
  - Feature availability
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/AboutPane.vue
---

# About

Authenticated application/engine versions and relevant instance information.
