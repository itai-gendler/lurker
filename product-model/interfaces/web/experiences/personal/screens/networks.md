---
entities:
- entity: network
  shows:
  - Name
  - Current nick
  - Connection state
  - Connection configuration
  - Connection preferences
  - Position
  collects:
  - Name
  - Connection configuration
  - Authentication
  - Connection preferences
  - Startup channels
  - Preferred nick
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
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/NetworksPane.vue
---

# Networks

Network configurations/states and offered presets. Collects add/order choices.
