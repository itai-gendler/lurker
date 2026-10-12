---
kind: primary
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The Administrator invokes setup lurker.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::login
    client-entry:
      place: client-api::public
  actor: administrator
- text: Valid first setup creates the initial Administrator account and session
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

# Setup lurker

## Trigger

The Administrator invokes setup lurker.

## Outcome

Valid first setup creates the initial Administrator account and session

The password setup path creates the first administrative account and its ordinary session. Web first setup has password input; the supported client API also exposes a passkey ceremony. The return destination is conditional.

## Edge cases

- Completed setup refuses another first account. An interrupted API passkey ceremony can leave provisional setup state.
