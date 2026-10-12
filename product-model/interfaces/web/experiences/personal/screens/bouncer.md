---
entities:
- entity: instance-settings
  shows:
  - Bouncer connection details
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
  target: vue_client/src/components/settings-panes/BouncerPane.vue
---

# Bouncer

Authenticated Instance Bouncer connection details.
