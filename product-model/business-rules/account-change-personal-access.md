---
appliesTo:
- type: entity
  id: account
  effect: changes
  contexts:
  - place: web::public
  - place: client-api::public
  - place: web::personal
  - place: client-api::personal
  facts:
  - Sign-in methods
  - Appearance settings
  - Chat settings
  - Event settings
  - Input bar settings
  - Upload settings
  - Notification settings
  - Away settings
  - Data settings
permits:
- related:
  - verb: has-account
    entity: user
  configuredBy: account
- related:
  - verb: has-account
    entity: administrator
  configuredBy: account
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

# Only the owning Account’s authenticated path or valid recovery changes its personal information

For ordinary personal HTTP changes, the acting principal must be the governed account and be unpaused. Settings persist only supported validated registry values. Password replacement requires proof of the current password when a password already exists; establishing a first password does not invent that extra requirement. Personal password removal requires a registered passkey. Passkey removal requires another passkey or a password. These continuity checks concern the selected account’s actual methods.

For recovery, select the exact live presented recovery link and its target, with standalone recovery availability. Password input validates before spending the link. A recovery passkey uses the signed recovery-purpose challenge with the same link and account and successful WebAuthn verification; spending and enrollment keep their actual transaction/duplicate-credential behavior. Valid recovery replaces prior access and performs the established cleanup rather than demanding an existing ordinary session.

The Account-configured alternative evaluates the dispatched path and its actual proof; it does not permit an authenticated owner to skip recovery proof or a public caller to edit arbitrary preferences.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
