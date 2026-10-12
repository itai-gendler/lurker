---
appliesTo:
- type: entity
  id: session
  effect: removes
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
- unattended: true
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
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Only presented logout, valid recovery or expiry cleanup removes the selected Session

The Session-configured holder grant permits logout removal only of the actual presented ordinary cookie/bearer session. Logout bypasses the paused HTTP-write gate; it does not permit deleting arbitrary sessions. The Account-configured recovery alternative requires the exact valid standalone recovery proof for the session owner and removes that owner’s previous sessions before fresh issuance and explicit socket cleanup.

Unattended cleanup removes expired ordinary sessions under their actual expiry policy. Ordinary logout and password change do not establish global closure of already-authenticated sockets. OAuth-token logout is separately governed OAuth access removal.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
