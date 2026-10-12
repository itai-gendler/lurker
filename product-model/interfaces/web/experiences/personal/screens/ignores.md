---
entities:
- entity: ignore-rule
  shows:
  - Mask
  - Pattern
  - Matching kind
  - Network scope
  - Levels
  - Exception status
  - Expires at
  collects:
  - Mask
  - Pattern
  - Matching kind
  - Network scope
  - Levels
  - Exception status
  - Expires at
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/IgnoresPane.vue
---

# Ignores

Match, level, exception, scope and expiry facts. Collects ignore inputs.
