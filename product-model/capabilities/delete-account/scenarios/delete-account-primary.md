---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes delete account.
  kind: actor
  entities:
  - entity: account
    effect: reads
    as: active-target
    facts: []
  - entity: account
    effect: reads
    as: paused-target
    facts: []
  contexts:
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: When the permitted target is active, the Product disposes its live access and removes that target with its
    dependent records in their current listed states.
  kind: product
  entities:
  - entity: account
    effect: removes
    from: Active
    as: active-target
  - entity: session
    effect: removes
    with: active-target
    from: Issued
    as: active-session
  - entity: passkey
    effect: removes
    with: active-target
    from: Registered
    as: active-passkey
  - entity: api-token
    effect: removes
    with: active-target
    from: Active
    as: active-api-token-active
  - entity: api-token
    effect: removes
    with: active-target
    from: Revoked
    as: active-api-token-revoked
  - entity: authorized-app
    effect: removes
    with: active-target
    from: Approved
    as: active-authorized-app
  - entity: network
    effect: removes
    with: active-target
    as: active-network
  - entity: nick-note
    effect: removes
    with: active-target
    as: active-nick-note
  - entity: relay-bot
    effect: removes
    with: active-target
    as: active-relay-bot
  - entity: highlight-rule
    effect: removes
    with: active-target
    as: active-highlight-rule
  - entity: ignore-rule
    effect: removes
    with: active-target
    as: active-ignore-rule
  - entity: theme
    effect: removes
    with: active-target
    as: active-theme
  - entity: personal-uploader
    effect: removes
    with: active-target
    as: active-personal-uploader
  - entity: image-upload
    effect: removes
    with: active-target
    as: active-image-upload
  - entity: file-upload
    effect: removes
    with: active-target
    as: active-file-upload
  - entity: web-push-subscription
    effect: removes
    with: active-target
    as: active-web-push-subscription
  - entity: native-push-device
    effect: removes
    with: active-target
    as: active-native-push-device
  - entity: data-export
    effect: removes
    with: active-target
    from: Pending
    as: active-data-export-pending
  - entity: data-export
    effect: removes
    with: active-target
    from: Running
    as: active-data-export-running
  - entity: data-export
    effect: removes
    with: active-target
    from: Ready
    as: active-data-export-ready
  - entity: data-export
    effect: removes
    with: active-target
    from: Failed
    as: active-data-export-failed
  - entity: bookmark
    effect: removes
    with: active-target
    as: active-bookmark
  - entity: draft
    effect: removes
    with: active-target
    as: active-draft
  - entity: pin
    effect: removes
    with: active-target
    as: active-pin
  - entity: favorite-buffer
    effect: removes
    with: active-target
    as: active-favorite-buffer
  - entity: recovery-link
    effect: removes
    with: active-target
    from: Issued
    as: active-recovery-link
  - entity: irc-client
    effect: removes
    with: active-target
    from: Registering
    as: active-irc-client-registering
  - entity: irc-client
    effect: removes
    with: active-target
    from: Attached
    as: active-irc-client-attached
  - entity: network-certificate
    effect: removes
    with: active-network
    from: Attached
    as: active-network-certificate
  - entity: channel
    effect: removes
    with: active-network
    from: Open
    as: active-channel-open
  - entity: channel
    effect: removes
    with: active-network
    from: Closed
    as: active-channel-closed
  - entity: direct-message
    effect: removes
    with: active-network
    from: Open
    as: active-direct-message-open
  - entity: direct-message
    effect: removes
    with: active-network
    from: Closed
    as: active-direct-message-closed
  - entity: network-log
    effect: removes
    with: active-network
    as: active-network-log
  - entity: message
    effect: removes
    with: active-network
    from: Recorded
    as: active-message
  - entity: irc-user
    effect: removes
    with: active-network
    as: active-irc-user
  - entity: reaction
    effect: removes
    with: active-message
    from: Active
    as: active-reaction-active
  - entity: reaction
    effect: removes
    with: active-message
    from: Withdrawn
    as: active-reaction-withdrawn
  - entity: lurker-log
    as: active-lurker-log
    effect: removes
    with: active-target
  - entity: invite
    as: active-issued-invite-available
    effect: removes
    from: Available
    with: active-target
  - entity: invite
    as: active-issued-invite-consumed
    effect: removes
    from: Consumed
    with: active-target
  contexts:
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: When the permitted target is paused, the Product disposes its live access and removes that target with its
    dependent records in their current listed states.
  kind: product
  entities:
  - entity: account
    effect: removes
    from: Paused
    as: paused-target
  - entity: session
    effect: removes
    with: paused-target
    from: Issued
    as: paused-session
  - entity: passkey
    effect: removes
    with: paused-target
    from: Registered
    as: paused-passkey
  - entity: api-token
    effect: removes
    with: paused-target
    from: Active
    as: paused-api-token-active
  - entity: api-token
    effect: removes
    with: paused-target
    from: Revoked
    as: paused-api-token-revoked
  - entity: authorized-app
    effect: removes
    with: paused-target
    from: Approved
    as: paused-authorized-app
  - entity: network
    effect: removes
    with: paused-target
    as: paused-network
  - entity: nick-note
    effect: removes
    with: paused-target
    as: paused-nick-note
  - entity: relay-bot
    effect: removes
    with: paused-target
    as: paused-relay-bot
  - entity: highlight-rule
    effect: removes
    with: paused-target
    as: paused-highlight-rule
  - entity: ignore-rule
    effect: removes
    with: paused-target
    as: paused-ignore-rule
  - entity: theme
    effect: removes
    with: paused-target
    as: paused-theme
  - entity: personal-uploader
    effect: removes
    with: paused-target
    as: paused-personal-uploader
  - entity: image-upload
    effect: removes
    with: paused-target
    as: paused-image-upload
  - entity: file-upload
    effect: removes
    with: paused-target
    as: paused-file-upload
  - entity: web-push-subscription
    effect: removes
    with: paused-target
    as: paused-web-push-subscription
  - entity: native-push-device
    effect: removes
    with: paused-target
    as: paused-native-push-device
  - entity: data-export
    effect: removes
    with: paused-target
    from: Pending
    as: paused-data-export-pending
  - entity: data-export
    effect: removes
    with: paused-target
    from: Running
    as: paused-data-export-running
  - entity: data-export
    effect: removes
    with: paused-target
    from: Ready
    as: paused-data-export-ready
  - entity: data-export
    effect: removes
    with: paused-target
    from: Failed
    as: paused-data-export-failed
  - entity: bookmark
    effect: removes
    with: paused-target
    as: paused-bookmark
  - entity: draft
    effect: removes
    with: paused-target
    as: paused-draft
  - entity: pin
    effect: removes
    with: paused-target
    as: paused-pin
  - entity: favorite-buffer
    effect: removes
    with: paused-target
    as: paused-favorite-buffer
  - entity: recovery-link
    effect: removes
    with: paused-target
    from: Issued
    as: paused-recovery-link
  - entity: irc-client
    effect: removes
    with: paused-target
    from: Registering
    as: paused-irc-client-registering
  - entity: irc-client
    effect: removes
    with: paused-target
    from: Attached
    as: paused-irc-client-attached
  - entity: network-certificate
    effect: removes
    with: paused-network
    from: Attached
    as: paused-network-certificate
  - entity: channel
    effect: removes
    with: paused-network
    from: Open
    as: paused-channel-open
  - entity: channel
    effect: removes
    with: paused-network
    from: Closed
    as: paused-channel-closed
  - entity: direct-message
    effect: removes
    with: paused-network
    from: Open
    as: paused-direct-message-open
  - entity: direct-message
    effect: removes
    with: paused-network
    from: Closed
    as: paused-direct-message-closed
  - entity: network-log
    effect: removes
    with: paused-network
    as: paused-network-log
  - entity: message
    effect: removes
    with: paused-network
    from: Recorded
    as: paused-message
  - entity: irc-user
    effect: removes
    with: paused-network
    as: paused-irc-user
  - entity: reaction
    effect: removes
    with: paused-message
    from: Active
    as: paused-reaction-active
  - entity: reaction
    effect: removes
    with: paused-message
    from: Withdrawn
    as: paused-reaction-withdrawn
  - entity: lurker-log
    as: paused-lurker-log
    effect: removes
    with: paused-target
  - entity: invite
    as: paused-issued-invite-available
    effect: removes
    from: Available
    with: paused-target
  - entity: invite
    as: paused-issued-invite-consumed
    effect: removes
    from: Consumed
    with: paused-target
  contexts:
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/index.ts
---

# Delete account

## Trigger

The Administrator invokes delete account.

## Outcome

Permitted target’s live access and account/dependents removed

Permitted account removal disposes live access before deleting dependent retained data. Self and final-administrator deletion are refused.

Either an active or paused permitted target can be removed. The Account-issued invitation rows and its personal Lurker-log view/events are cleaned under their parent relationship. The database also cascades invitation rows whose admitted member is the removed target; that does not remove the other issuer’s account. The dependent cleanup is scoped to that removed account and its networks; application registrations, shared global Product events, instance policy and remote provider bytes are not represented as deleted.

## Decision points

### Selected target state

Is the eligible target active or paused?

- Active target → remove that selected account and its dependent records.
- Paused target → remove that selected account and its dependent records.
