---
entities:
- entity: invite
  shows:
  - Expires at
  - Validity
- entity: account
  collects:
  - Username
  - Sign-in methods
references:
- kind: code
  role: implementation
  target: vue_client/src/views/InviteAccept.vue
- kind: code
  role: implementation
  target: server/routes/auth.ts
entryPoints:
- web: /invite/:token
---

# Invite

Valid Invite expiry/validity. Collects account and sign-in input.
