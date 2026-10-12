---
kind: primary
result: achieved
routes:
  web: Web
steps:
- text: The User selects an eligible archive and confirms replacement of personal data.
  kind: actor
  entities: []
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: The Product replaces the prior personal preferences and saved themes before restoring the archive’s supported
    values.
  kind: product
  entities:
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
  - entity: theme
    effect: removes
    as: prior-theme
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: For rows actually carried by the archive, the Product restores rekeyed connection configurations, conversation
    visibility, personal annotations, ordering, upload history and credential-less destinations.
  kind: product
  entities:
  - entity: network
    effect: creates
    facts:
    - Name
    - Connection configuration
    - Authentication
    - Connection preferences
    - Preferred nick
    - Away state
    - CASEMAPPING
    - Position
  - entity: network-certificate
    effect: creates
    to: Attached
    with: network
    facts:
    - Certificate description
    - Certificate
    - Private credential
  - entity: channel
    effect: creates
    as: restored-channel-open
    to: Open
    with: network
    facts:
    - Target
    - Visibility
    - Joined status
    - Autojoin
    - Channel key
    - Topic
    - Members
    - Modes
    - Mode lists
    - Read boundary
    - Clear boundary
    - Unread counts
    - Retention override
    - Notification override
    - Encryption status
    - Events
  - entity: channel
    effect: creates
    as: restored-channel-closed
    to: Closed
    with: network
    facts:
    - Target
    - Visibility
    - Joined status
    - Autojoin
    - Channel key
    - Topic
    - Members
    - Modes
    - Mode lists
    - Read boundary
    - Clear boundary
    - Unread counts
    - Retention override
    - Notification override
    - Encryption status
    - Events
  - entity: direct-message
    effect: creates
    as: restored-direct-message-open
    to: Open
    with: network
    facts:
    - Target
    - Visibility
    - Peer presence
    - Read boundary
    - Clear boundary
    - Unread counts
    - Retention override
    - Events
  - entity: direct-message
    effect: creates
    as: restored-direct-message-closed
    to: Closed
    with: network
    facts:
    - Target
    - Visibility
    - Peer presence
    - Read boundary
    - Clear boundary
    - Unread counts
    - Retention override
    - Events
  - entity: nick-note
    effect: creates
    with: network
    facts:
    - Nick
    - Text
    - Updated at
  - entity: relay-bot
    effect: creates
    with: network
    facts:
    - Nick
    - Envelope template
    - Created at
  - entity: theme
    effect: creates
    facts:
    - Name
    - Values
    - Created at
    - Updated at
    as: restored-theme
  - entity: highlight-rule
    effect: creates
    facts:
    - Pattern
    - Mask
    - Matching kind
    - Network scope
    - Channel scope
    - Case sensitivity
    - Enabled
    - Automatic origin
  - entity: ignore-rule
    effect: creates
    facts:
    - Mask
    - Pattern
    - Matching kind
    - Network scope
    - Levels
    - Exception status
    - Expires at
  - entity: personal-uploader
    effect: creates
    facts:
    - Label
    - Driver
    - Configuration
    - Secrets
    - Secret status
    - Enabled
  - entity: draft
    effect: creates
    facts:
    - Text
    - Reply reference
    - Updated at
  - entity: pin
    effect: creates
    facts:
    - Position
  - entity: favorite-buffer
    effect: creates
    facts:
    - Position
  - entity: account
    effect: reads
    facts:
    - Data settings
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: The Product restores the archive’s image or file history records independently of whether their prior destination
    can be mapped.
  kind: product
  entities:
  - entity: image-upload
    effect: creates
    facts:
    - Filename
    - URL
    - Content type
    - Byte size
    - Dimensions
    - Thumbnail
    - Deletion reference
    - Favorite status
    - Removal status
  - entity: file-upload
    effect: creates
    facts:
    - Filename
    - URL
    - Content type
    - Byte size
    - Deletion reference
    - Favorite status
    - Removal status
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: Only when the optional history is present and the referenced rows map, the Product restores retained content
    and its saved associations.
  kind: product
  entities:
  - entity: message
    effect: creates
    to: Recorded
    facts:
    - Sender
    - Content
    - Kind
    - Time
    - Self attribution
    - Upstream identity
    - Reply context
    - Highlight information
    - Ignore information
    - Encryption indication
  - entity: reaction
    effect: creates
    to: Active
    with: message
    facts:
    - Value
    - Reacting identity
    - Self attribution
    - Reacted at
    - Removed at
  - entity: bookmark
    effect: creates
    with: message
    facts:
    - Saved at
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: For supported mapped anchors and overrides present in the archive, the Product restores the addressed conversation’s
    read, clear and inherited-setting facts.
  kind: product
  entities:
  - entity: channel
    effect: changes
    as: restored-channel-open
    facts:
    - Read boundary
    - Clear boundary
    - Retention override
    - Notification override
  - entity: channel
    effect: changes
    as: restored-channel-closed
    facts:
    - Read boundary
    - Clear boundary
    - Retention override
    - Notification override
  - entity: direct-message
    effect: changes
    as: restored-direct-message-open
    facts:
    - Read boundary
    - Clear boundary
    - Retention override
  - entity: direct-message
    effect: changes
    as: restored-direct-message-closed
    facts:
    - Read boundary
    - Clear boundary
    - Retention override
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: The web data view resets chat state, replaces its route with / and reloads.
  kind: product
  entities: []
  contexts:
    web:
      place: web::personal::data
  actor: user
  capability: import-data
- text: The User opens the restored personal buffer list after reload.
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
    as: restored-channel-open
  - entity: direct-message
    effect: reads
    facts:
    - Target
    - Visibility
    - Unread counts
    as: restored-direct-message-open
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
  target: vue_client/src/components/settings-panes/DataPane.vue
- kind: code
  role: implementation
  target: server/routes/exports.ts
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
---

# Import to chat achieved

## Trigger

Import an eligible archive and arrive in usable restored chat.

## Outcome

Replacement succeeds, web client state is reset, and the carried person can browse restored buffers.

## Decision points

### Archive contents

Does the restored archive include usable message history?

- Usable history present → the destination includes mapped retained messages and supported associations.
- History absent → the destination includes restored personal configuration without unresolvable history associations.
