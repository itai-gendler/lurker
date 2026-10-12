---
entities:
- entity: highlight-rule
  shows:
  - Pattern
  - Mask
  - Matching kind
  - Network scope
  - Channel scope
  - Case sensitivity
  - Enabled
  - Automatic origin
  collects:
  - Pattern
  - Mask
  - Matching kind
  - Network scope
  - Channel scope
  - Case sensitivity
  - Enabled
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
---

# Highlight rules

Match, scope, enabled and automatic-origin facts. Collects editable fields.
