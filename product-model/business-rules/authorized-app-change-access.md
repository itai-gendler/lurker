---
appliesTo:
- type: entity
  id: authorized-app
  effect: changes
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
- related:
  - verb: has-authorization
    entity: client-application
  configuredBy: client-application
- unattended: true
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

# Only exact approval exchange, token use or permitted revocation changes its Authorized-app access

The Client-application-configured exchange grant selects the actual registered client named in the request and the exact presented authorization code. Resolve the client before consuming the code. Consume a live code once (ten-minute expiry), then require its app identity, return location and S256 verifier equal those of that request. A later mismatch still consumes that code. Successful exchange issues nonexpiring access bound to that code’s account and application; the public client ID alone is not authentication.

The Account-configured owner alternative is only an authenticated account’s supported access management/logout path. Personal management writes require that current account unpaused; logout instead revokes only the presented OAuth token and bypasses the pause-write guard. It never lets an owner mint a token without the code/PKCE exchange.

Attributable token use updates only the matched issued access’s last-use time. OAuth revocation selects the exact presented token and matching registered client, deletes that access when matched, and closes its associated sockets. No token refresh or automatic access expiry is asserted.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
