---
kind: primary
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User invokes accept invite.
  kind: actor
  entities:
  - entity: invite
    effect: reads
    facts: []
  contexts: &id001
    web-public:
      place: web::public::invite
    client-entry:
      place: client-api::public
  actor: user
- text: Valid invitation is consumed; account and session created
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
- text: The Product completes the established web hand-off into usable chat.
  kind: product
  entities: []
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

# Accept invite

## Trigger

The User invokes accept invite.

## Outcome

Valid invitation is consumed; account and session created

The successful password path consumes the invitation and issues account access. Web success carries the person into chat; passkey redemption is separately exposed through the client API.

## Edge cases

- Unknown, expired and consumed invitations fail without admitting another account.
