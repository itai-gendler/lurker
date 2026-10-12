---
entities:
- entity: instance-settings
  shows:
  - Setup status
  - Sign-in availability
  - Feature availability
- entity: account
  collects:
  - Username
  - Sign-in methods
references:
- kind: code
  role: implementation
  target: vue_client/src/views/Login.vue
- kind: code
  role: implementation
  target: server/routes/auth.ts
entryPoints:
- web: /login
---

# Login

Instance Setup status and Sign-in availability. Collects username, password or passkey proof and first-run account input.
