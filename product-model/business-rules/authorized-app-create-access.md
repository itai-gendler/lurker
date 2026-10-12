---
appliesTo:
- type: entity
  id: authorized-app
  effect: creates
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

# Only the matching cookie Account approves the selected application

The Account-configured owner grant requires a valid signed ordinary-session cookie and the current account unpaused; no bearer substitutes for human approval. Resolve the actual registered application, accepted return location and S256 challenge. Approval requires both the displayed account identity and displayed username equal the actual cookie-authenticated account. The resulting association/code belongs to that account and application.

The approval-only comparison is not added to denial: the supported denial path returns access_denied before that displayed-account check and creates no authorization. Public client ID identifies the application; it does not authenticate it.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
