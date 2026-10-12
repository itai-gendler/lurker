---
appliesTo:
- type: entity
  id: account
  effect: reads
  contexts:
  - place: web::public
  - place: client-api::public
  facts:
  - Username
  - Sign-in methods
permits:
- actors:
  - user
  - administrator
  configuredBy: recovery-link
references:
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/db/sessions.ts#findSession
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Only the valid recovery proof discloses its limited Account entry information

The Recovery-link-configured grant selects the exact hash-matched, still-live presented recovery link and its target account in standalone edition. The landing projection reveals that account’s username and password-presence indication, with the link expiry, only while that proof is valid. Unknown and expired links do not disclose that an account had a link. No ordinary anonymous account-name query receives private sign-in methods: the login surface advertises only the instance aggregate.
