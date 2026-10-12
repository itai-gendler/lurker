---
kind: primary
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User invokes recover account.
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
- text: Valid recovery replaces prior access and issues a fresh session
  kind: product
  entities:
  - entity: recovery-link
    effect: removes
    from: Issued
  - entity: account
    effect: changes
    facts:
    - Sign-in methods
  - entity: session
    effect: removes
    from: Issued
    as: prior-session
  - entity: passkey
    effect: removes
    from: Registered
    as: prior-passkey
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

# Recover account

## Trigger

The User invokes recover account.

## Outcome

Valid recovery replaces prior access and issues a fresh session

Recovery consumes the single-use proof, replaces prior password/passkey access, invalidates ordinary sessions, revokes delegated access and closes associated live access. A separate completion step issues fresh access. Web success returns into chat.

## Edge cases

- No email delivery is promised; an administrator hands the recovery URL to the person. New issuance supersedes earlier links.
