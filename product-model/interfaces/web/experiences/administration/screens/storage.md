---
entities:
- entity: instance-settings
  shows:
  - Storage measurements
  - Retention ceilings
- entity: account
  shows:
  - Retained history counts
  - Username
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Storage

Storage attribution, retention ceilings and retained-history counts.
