---
appliesTo:
- type: entity
  id: client-application
  effect: changes
permits:
- actors:
  - user
  - administrator
  configuredBy: account
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/db/sessions.ts#findSession
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireCookieSession
---

# Only the matching cookie Account records the selected application’s first approval

The Account-configured grant applies only to human approval for the actual resolved registration. Require the valid signed session cookie, current account unpaused, accepted application return location/S256 challenge and approval decision. Both displayed account identity and username must equal the actual cookie account before createCode marks First approval. Denial precedes that comparison and does not change First approval. A public client ID does not authenticate the application or authorize unrelated registration edits.
