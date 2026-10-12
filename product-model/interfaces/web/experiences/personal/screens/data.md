---
entities:
- entity: account
  shows:
  - Data settings
  collects:
  - Data settings
- entity: data-export
  shows:
  - Requested contents
  - Progress
  - Counts
  - Artifact
  - Error
  - Expires at
  - Downloaded at
  collects:
  - Requested contents
- entity: instance-settings
  shows:
  - Retention ceilings
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/DataPane.vue
entryPoints:
- web: /settings/data
---

# Data

Account Data settings, export progress/artifact and retention ceilings. Collects settings, export contents and archive input.
