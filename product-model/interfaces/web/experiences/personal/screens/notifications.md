---
entities:
- entity: account
  shows:
  - Notification settings
  collects:
  - Notification settings
- entity: web-push-subscription
  shows:
  - Device description
  - Enabled
  - Last seen at
  - Delivery health
- entity: native-push-device
  shows:
  - Transport
  - Device description
  - Enabled
  - Last seen at
  - Delivery health
- entity: instance-settings
  shows:
  - Notification transports
  - Relay opt-in
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/NotificationsPane.vue
---

# Notifications

Account Notification settings and subscription description/health. Collects preferences and registration; delivery keys are not displayed.
