---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User starts an eligible import that fails after member identity-data replacement has begun.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: After replacement has begun and insertion fails, the Product clears imported connection roots and dependent
    records plus personal preference, theme, highlight, destination and upload-history roots.
  kind: product
  entities:
  - entity: network
    effect: removes
  - entity: network-certificate
    effect: removes
    with: network
    from: Attached
  - entity: channel
    effect: removes
    with: network
    from: Open
    as: channel-open
  - entity: channel
    effect: removes
    with: network
    from: Closed
    as: channel-closed
  - entity: direct-message
    effect: removes
    with: network
    from: Open
    as: direct-message-open
  - entity: direct-message
    effect: removes
    with: network
    from: Closed
    as: direct-message-closed
  - entity: network-log
    effect: removes
    with: network
  - entity: message
    effect: removes
    with: network
    from: Recorded
  - entity: irc-user
    effect: removes
    with: network
  - entity: nick-note
    effect: removes
    with: network
  - entity: relay-bot
    effect: removes
    with: network
  - entity: reaction
    effect: removes
    with: message
    from: Active
    as: reaction-active
  - entity: reaction
    effect: removes
    with: message
    from: Withdrawn
    as: reaction-withdrawn
  - entity: highlight-rule
    effect: removes
  - entity: theme
    effect: removes
  - entity: personal-uploader
    effect: removes
  - entity: account
    effect: changes
    facts:
    - Appearance settings
    - Chat settings
    - Event settings
    - Input bar settings
    - Upload settings
    - Notification settings
    - Away settings
    - Data settings
  contexts: *id001
  actor: user
- text: The Product independently clears the account’s imported image and file history metadata without deleting
    remote provider bytes.
  kind: product
  entities:
  - entity: image-upload
    effect: removes
  - entity: file-upload
    effect: removes
  - entity: account
    effect: reads
    facts:
    - Data settings
  contexts:
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/exports.ts
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/DataPane.vue
- kind: code
  role: implementation
  target: server/db/index.ts
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
---

# Import data partial failure cleanup

## Trigger

The User starts an eligible import that fails after account-data replacement has begun.

## Outcome

Imported parents and dependent content are cleaned after mutation begins. Original zero-network preferences/themes were replaced and are not restored by that cleanup.

The reset is account-scoped. Conversation-dependent drafts, ordering and bookmarks disappear with the deleted buffers/history. Upload cleanup removes metadata, not provider bytes, and does not invoke the interactive provider-deletion ceremony. Original preferences and saved themes are not restored. No successful import hand-off follows this failure.
