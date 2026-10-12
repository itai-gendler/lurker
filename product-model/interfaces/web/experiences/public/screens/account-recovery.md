---
entities:
- entity: recovery-link
  shows:
  - Expires at
  - Validity
- entity: account
  shows:
  - Username
  - Sign-in methods
  collects:
  - Sign-in methods
- entity: passkey
  collects:
  - Registration
references:
- kind: code
  role: implementation
  target: vue_client/src/views/AccountRecovery.vue
- kind: code
  role: implementation
  target: server/routes/auth.ts
entryPoints:
- web: /recover/:token
---

# Account recovery

Valid recovery-link information, username and password presence. Collects replacement sign-in method.
