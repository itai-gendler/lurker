---
entities:
- entity: account
  shows:
  - Upload settings
  collects:
  - Upload settings
- entity: personal-uploader
  shows:
  - Label
  - Driver
  - Configuration
  - Secret status
  - Enabled
  collects:
  - Label
  - Driver
  - Configuration
  - Secrets
  - Enabled
- entity: instance-uploader
  shows:
  - Label
  - Driver
  - Enabled
  - Default status
  - Offered to users
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
---

# Uploads settings

Account Upload settings; personal uploader configuration/secret status; offered instance metadata. Collects settings, selection and configuration.
