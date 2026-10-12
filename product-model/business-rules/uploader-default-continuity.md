---
appliesTo:
- type: entity
  id: instance-uploader
- type: entity
  id: instance-settings
references:
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
- kind: code
  role: implementation
  target: server/routes/config.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/app.ts
---

# Uploader default continuity

The enabled usable instance default cannot be disabled or removed until an allowed replacement is assigned. Built-in destinations cannot be removed; managed configuration is locked. Disabling personal creation does not forbid later edit/removal of existing personal rows.
