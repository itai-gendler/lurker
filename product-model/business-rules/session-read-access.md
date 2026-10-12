---
appliesTo:
- type: entity
  id: session
  effect: reads
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  configuredBy: session
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  configuredBy: session
references:
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/db/sessions.ts#findSession
---

# Only the presented ordinary session identifies its bound Account on an accepting surface

The Session-configured grant selects the exact presented opaque credential, resolves its retained session and owner, and rejects absent or expired sessions. A signed cookie must verify; an ordinary bearer is accepted only through the supported bearer path. The credential’s owner must be the acting account. A 30-day expiry is checked at lookup, not promised as forced expiry of an already-open socket. MCP API tokens and bouncer passwords are separate credentials, and no account may choose another owned session to authenticate an invalid presented value.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
