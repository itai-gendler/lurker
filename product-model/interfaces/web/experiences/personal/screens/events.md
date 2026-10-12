---
entities:
- entity: account
  shows:
  - Event settings
  collects:
  - Event settings
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
---

# Events

Account Event settings. Collects changes.
