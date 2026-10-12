---
entities:
- entity: instance-settings
  shows:
  - Notification transports
  - Relay opt-in
  - Relay status
  collects:
  - Relay opt-in
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/NotificationsPane.vue
---

# Notifications

Transport availability, Relay opt-in/status. Collects policy and explicit status check.
