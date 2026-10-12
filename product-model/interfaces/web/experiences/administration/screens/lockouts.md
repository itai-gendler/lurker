---
entities:
- entity: instance-settings
  shows:
  - Blocked sign-ins
  - Login policy
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Lockouts

Instance Blocked sign-ins and Login policy. Collects clear-blocked request.
