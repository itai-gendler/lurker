---
kind: path
routes:
  client-entry: Client entry
steps:
- text: The Administrator requests first setup with a WebAuthn proof through the client member identity-entry
    ceremony.
  kind: actor
  entities: []
  contexts: &id001
    client-entry:
      place: client-api::public
  actor: administrator
- text: Cookie-backed passkey setup ceremony creates initial access
  kind: product
  entities:
  - entity: account
    effect: creates
    facts:
    - Username
    - Sign-in methods
    - Pause status
    - Ident
    - Appearance settings
    - Chat settings
    - Event settings
    - Input bar settings
    - Upload settings
    - Notification settings
    - Away settings
    - Data settings
    - Retained history counts
    to: Active
  - entity: passkey
    effect: creates
    facts:
    - Label
    - Registration
    - Device information
    - Created at
    - Last used at
    to: Registered
    with: account
  - entity: session
    effect: creates
    facts:
    - Credential
    - Issued at
    - Expires at
    to: Issued
    with: account
  contexts: *id001
  actor: administrator
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
---

# Setup lurker passkey api

## Trigger

The Administrator requests first setup with a passkey through the client account-entry ceremony.

## Outcome

Cookie-backed passkey setup ceremony creates initial access
