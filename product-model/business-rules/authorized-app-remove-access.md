---
appliesTo:
- type: entity
  id: authorized-app
  effect: removes
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
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Only the authenticated owner or its valid recovery revokes the selected Authorized app

Account-configured personal revocation requires the actual authenticated owner unpaused and the selected registered app’s authorization within that account. Remove that pair’s outstanding codes/tokens, close sockets identified by the removed access tokens, and remove their OAuth-bound push registrations.

The Account-configured recovery path instead requires the exact valid standalone recovery proof for that same target account and performs the broader established access replacement. This is not an ordinary owner bypass of recovery proof. Public client IDs or administrative role alone confer no other-account authorization removal.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
