---
entities:
- entity: network-preset
  shows:
  - Name
  - Host
  - Port
  - TLS
  - Recommended channels
  - Authentication guidance
  - Enabled
  - Position
  collects:
  - Name
  - Host
  - Port
  - TLS
  - Recommended channels
  - Authentication guidance
  - Enabled
  - Position
- entity: instance-settings
  shows:
  - Network policy
  collects:
  - Network policy
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/NetworksPane.vue
---

# Networks

Preset facts and Network policy. Collects preset/policy changes.
