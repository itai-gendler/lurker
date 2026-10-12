---
kind: primary
result: achieved
routes:
  web: Web
steps:
- text: The User presents the live recovery link and a validated replacement password.
  kind: actor
  entities:
  - entity: account
    effect: reads
    facts: []
  - entity: recovery-link
    effect: reads
    facts:
    - Validity
    - Expires at
  contexts:
    web:
      place: web::public::account-recovery
  actor: user
  capability: recover-account
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
  contexts:
    web:
      place: web::public::account-recovery
  actor: user
  capability: recover-account
- text: The Product independently removes all prior push registrations.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: removes
  - entity: native-push-device
    effect: removes
  contexts:
    web:
      place: web::public::account-recovery
  actor: user
  capability: recover-account
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
  contexts:
    web:
      place: web::public::account-recovery
  actor: user
  capability: recover-account
- text: After web recovery succeeds, the Product establishes the fresh session and the web client returns to chat;
    the API returns issued access.
  kind: product
  entities:
  - entity: session
    effect: reads
    as: fresh-session
    facts:
    - Credential
  contexts:
    web:
      place: web::public::account-recovery
  actor: user
  capability: recover-account
- text: The recovery view establishes the fresh session and navigates to personal chat.
  kind: product
  entities:
  - entity: session
    effect: reads
    as: fresh-session
    facts:
    - Credential
  contexts:
    web:
      place: web::public::account-recovery
  actor: user
  capability: recover-account
- text: The User opens the personal buffer list after recovery.
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
  target: vue_client/src/views/AccountRecovery.vue
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

# Recovery to chat achieved

## Trigger

Replace compromised sign-in access and arrive in usable personal chat.

## Outcome

The recovery replacement completes, fresh access is issued, and the carried person can browse their buffers.
