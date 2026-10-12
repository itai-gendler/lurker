---
appliesTo:
- type: entity
  id: session
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
- actors:
  - user
  - administrator
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

# Only successful supported account entry issues the resulting Account session

The Account-configured grants use the actual account established by the completed entry path: valid password or signed passkey login; eligible first setup; exact valid invitation redemption; or exact valid standalone recovery. Password authentication verifies that username’s actual configured password. Passkey login consumes its signed login-purpose challenge and verifies the registered credential, expected challenge/origin/RP and account association. Credential failure/throttling denies entry.

Setup/invitation/recovery ceremonies retain their distinct proof, race and provisional-account boundaries. Successful issuance creates the ordinary 30-day session for the resulting account, not an arbitrary account related to the caller. Paused ordinary login is not categorically refused by these login handlers; later surface write guards still apply.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
