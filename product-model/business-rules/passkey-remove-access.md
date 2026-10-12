---
appliesTo:
- type: entity
  id: passkey
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
  target: server/db/webauthnCredentials.ts
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
  target: server/services/webauthn.ts#consumeChallenge
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Only the authenticated owner with another method or valid recovery removes its Passkey

Personal HTTP removal requires the authenticated account unpaused and the selected credential owned by it. If at most one passkey remains and the account has no password, refuse before removal. A password or another registered passkey preserves personal sign-in continuity.

Valid standalone recovery instead selects the exact live presented recovery link and its target account and replaces old methods under the supported password or signed passkey recovery ceremony. Recovery can clear prior passkeys without the personal last-method condition because it establishes the replacement method. Parent account deletion requires its independent administrative target checks.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
