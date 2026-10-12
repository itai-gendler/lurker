---
kind: path
routes:
  client-entry: Client entry
steps:
- text: The User chooses WebAuthn proof registration for the presented invitation through the client ceremony.
  kind: actor
  entities:
  - entity: invite
    effect: reads
    facts: []
  contexts: &id001
    client-entry:
      place: client-api::public
  actor: user
- text: Valid invitation redeemed through passkey API ceremony
  kind: product
  entities:
  - entity: invite
    effect: changes
    facts:
    - Redeemed at
    - Validity
    to: Consumed
    from: Available
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
  target: server/db/invites.ts
---

# Accept invite passkey api

## Trigger

The User chooses passkey registration for the presented invitation through the client ceremony.

## Outcome

Valid invitation redeemed through passkey API ceremony
