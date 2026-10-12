---
entities:
- entity: client-application
  shows:
  - Name
  - Website
  - Return locations
- entity: account
  shows:
  - Username
- entity: authorized-app
  collects:
  - Approval
references:
- kind: code
  role: implementation
  target: vue_client/src/views/OAuthAuthorize.vue
- kind: code
  role: implementation
  target: server/routes/oauth.ts
entryPoints:
- web: /oauth/authorize
---

# Application approval

Application name/website/return location and displayed account. Collects approval or denial.
