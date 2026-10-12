---
kind: exception
routes:
  client-entry: Client entry
steps:
- text: The Administrator starts WebAuthn proof setup, then interrupts or fails registration after the provisional
    first member identity has been created.
  kind: actor
  entities: []
  contexts: &id001
    client-entry:
      place: client-api::public
  actor: administrator
- text: The provisional first account can already exist before credential registration finishes. Interruption
    does not promise atomic rollback.
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

# Setup lurker incomplete passkey

## Trigger

The Administrator starts passkey setup, then interrupts or fails registration after the provisional first account has been created.

## Outcome

The provisional first account can already exist before credential registration finishes. Interruption does not promise atomic rollback.
