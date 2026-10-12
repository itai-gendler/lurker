---
appliesTo:
- type: entity
  id: passkey
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

# Only the matched Account ceremony registers its verified Passkey

The Account-configured personal grant selects the current authenticated, unpaused account and its pending add-passkey ceremony. Verification must receive the valid signed challenge cookie, consume an unexpired challenge whose purpose is add-passkey and whose account equals the authenticated caller, and successfully verify registration against the expected challenge, origin and RP. A bearer credential alone supplies no challenge proof.

The entry grant is limited to setup, invitation or recovery registration. Select the provisional or recovering account actually bound into that signed, unexpired purpose-specific challenge. Setup retains the no-existing-credentials race guard; invitation verification matches its exact presented invitation, rechecks liveness and consumes once; recovery verification matches its exact presented link and account and performs the established atomic spend/enroll replacement. It does not grant anonymous registration on an arbitrary existing account.

Challenges last five minutes, are consumed on verification lookup, and are cleared by process restart. They are authentication proof inputs, not kept validity facts on Account, Session or Passkey. User verification is preferred by registration options but verifyRegistrationResponse uses requireUserVerification:false; do not invent a mandatory verification flag.

On ordinary personal paths using requireAuth, the Account-configured alternative selects the actual account authenticated by the request: valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer. Public account-entry and recovery ceremonies instead establish identity through their exact proof described above; they do not require an existing ordinary session. The session must exist and be unexpired; OAuth access must still exist and resolve to that same account. API tokens are not ordinary REST credentials. Authentication selects a principal; proof inputs and challenge cookies are not new kept authorization facts.
