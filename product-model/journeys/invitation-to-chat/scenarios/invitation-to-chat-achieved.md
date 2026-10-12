---
kind: primary
result: achieved
routes:
  web: Web
steps:
- text: The User submits the invitation proof, username and supported replacement sign-in method.
  kind: actor
  entities:
  - entity: invite
    effect: reads
    facts: []
  contexts:
    web:
      place: web::public::invite
  actor: user
  capability: accept-invite
- text: The Product consumes the available invitation and issues the new account’s ordinary session.
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
  contexts:
    web:
      place: web::public::invite
  actor: user
  capability: accept-invite
- text: The invitation view establishes session state and navigates to personal chat.
  kind: product
  entities:
  - entity: session
    effect: reads
    facts:
    - Credential
  contexts:
    web:
      place: web::public::invite
  actor: user
  capability: accept-invite
- text: The User opens the personal buffer list after sign-in.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
  actor: user
  capability: browse-buffers
- text: The Product returns the selected destination’s retained conversation information.
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Target
    - Visibility
    - Unread counts
  - entity: direct-message
    effect: reads
    facts:
    - Target
    - Visibility
    - Unread counts
  - entity: network
    effect: reads
    facts:
    - Name
    - Current nick
    - Connection state
  contexts: *id001
  actor: user
  capability: browse-buffers
references:
- kind: code
  role: implementation
  target: vue_client/src/views/InviteAccept.vue
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

# Invitation to chat achieved

## Trigger

Accept an invitation and arrive in usable personal chat.

## Outcome

The invitation is consumed, account access is issued, and the carried person can browse their buffers.
