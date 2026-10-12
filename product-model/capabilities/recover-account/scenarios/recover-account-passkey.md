---
kind: path
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User answers the signed recovery challenge for the presented link with a replacement WebAuthn proof.
  kind: actor
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts: &id001
    web-public:
      place: web::public::account-recovery
    client-entry:
      place: client-api::public
  actor: user
- text: Valid recovery replaces access using a passkey
  kind: product
  entities:
  - entity: recovery-link
    effect: removes
    from: Issued
  - entity: account
    effect: changes
    facts:
    - Sign-in methods
  - entity: passkey
    effect: removes
    as: prior-passkey
    from: Registered
  - entity: session
    effect: removes
    from: Issued
    as: prior-session
  - entity: api-token
    effect: changes
    facts:
    - Revocation
    to: Revoked
    from: Active
  - entity: authorized-app
    effect: removes
    from: Approved
  - entity: irc-client
    effect: removes
    from: Attached
  contexts: *id001
  actor: user
- text: In the same credential-replacement transaction, the Product enrolls the validated replacement authenticator.
  kind: product
  entities:
  - entity: passkey
    effect: creates
    facts:
    - Label
    - Registration
    - Device information
    - Created at
    - Last used at
    to: Registered
    as: replacement-passkey
  contexts:
    web-public:
      place: web::public::account-recovery
    client-entry:
      place: client-api::public
  actor: user
- text: The Product independently removes all prior push registrations.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: removes
  - entity: native-push-device
    effect: removes
  contexts:
    web-public:
      place: web::public::account-recovery
    client-entry:
      place: client-api::public
  actor: user
- text: The Product issues fresh ordinary access after replacing the prior access.
  kind: product
  entities:
  - entity: session
    effect: creates
    facts:
    - Credential
    - Issued at
    - Expires at
    to: Issued
    as: fresh-session
  contexts: *id001
  actor: user
- text: After web recovery succeeds, the Product establishes the fresh session and the web client returns to chat;
    the API returns issued access.
  kind: product
  entities:
  - entity: session
    effect: reads
    as: fresh-session
    facts:
    - Credential
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
---

# Recover account passkey

## Trigger

The User answers the signed recovery challenge for the presented link with a replacement passkey.

## Outcome

Valid recovery replaces access using a passkey

## Edge cases

- A globally duplicate replacement credential returns 409; the credential-replacement transaction rolls back proof consumption, prior passkey removal and password clearing, so another authenticator can be tried. This does not claim atomic rollback of subsequent session/delegation/socket cleanup.
- The signed challenge must match the link’s target account; an unusable or mismatched proof leaves the credential replacement unperformed.
