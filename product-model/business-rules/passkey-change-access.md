---
appliesTo:
- type: entity
  id: passkey
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
---

# Only the authenticated owner changes its Passkey label

The personal HTTP rename requires the current authenticated account unpaused and a credential addressed within that account; updateLabel uses both credential and caller identities. Label input follows the supported normalization. Attributable successful passkey use may update only that credential’s observed usage/counter metadata under its verified account ceremony, not arbitrary caller-supplied credential data.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
