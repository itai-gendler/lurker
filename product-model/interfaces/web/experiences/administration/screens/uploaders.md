---
entities:
- entity: instance-uploader
  shows:
  - Label
  - Driver
  - Configuration
  - Secret status
  - Enabled
  - Offered to users
  - Default status
  - Managed status
  - Built-in status
  collects:
  - Label
  - Driver
  - Configuration
  - Secrets
  - Enabled
  - Offered to users
  - Default status
- entity: instance-settings
  shows:
  - Uploader policy
  collects:
  - Uploader policy
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Uploaders

Administrative uploader configuration/secret status and uploader policy. Collects configuration/default/policy changes.
