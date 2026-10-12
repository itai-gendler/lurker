---
appliesTo:
- type: entity
  id: authorized-app
  effect: reads
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  configuredBy: account
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
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

# Only the authenticated owning Account reads its Authorized-app associations

Account-configured disclosure lists only application associations under the actual authenticated account, using its currently retained issued-token rows and the selected app metadata. GET permits paused read access. Ordinary authentication or administrative role does not grant another account’s approvals, access tokens or secrets. Human approval preparation still requires the signed session cookie and its own registered-application/return/challenge validation.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
