---
entities:
- entity: authorized-app
  shows:
  - Approval
  - Last used at
- entity: client-application
  shows:
  - Name
  - Website
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/AuthorizedAppsPane.vue
- kind: code
  role: implementation
  target: server/db/oauth.ts#listAuthorizedApps
---

# Authorized apps

Application name/website and authorization/use information. Collects revocation.
