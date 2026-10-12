---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes import data.
  kind: actor
  entities: []
  contexts:
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
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
    client:
      place: client-api::personal
  actor: user
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
    client:
      place: client-api::personal
  actor: user
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
    client:
      place: client-api::personal
  actor: user
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
    client:
      place: client-api::personal
  actor: user
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
    client:
      place: client-api::personal
  actor: user
- text: After success, the web data view resets chat state, replaces the route with / and reloads; the API returns
    imported counts.
  kind: product
  entities: []
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
  target: server/db/exportSchema.ts
- kind: code
  role: implementation
  target: server/services/exportService.ts
---

# Import data

## Trigger

The User invokes import data.

## Outcome

Eligible validated archive replaces account data

An eligible validated archive replaces owned data with rekeyed parents and retained content. The account must have zero networks, but prior settings/themes can exist and are replaced.

## Edge cases

- Archive validation before replacement differs from failure after mutation starts. Partial-failure cleanup removes imported data without restoring original preferences/themes.
- Success carries the web client through session-state reset into chat; it does not promise atomic replacement, provider availability or immediate confirmed IRC registration.

## Contract details

The archive can carry portable network/channel connection secrets as plaintext, but omits personal-uploader secret values, local upload deletion handles, account sign-in credentials/roles/pause/ident, draft reply references and reaction-withdrawal tombstones. Imported personal destinations arrive credential-less and require re-entry. Upload records preserve URL/history rather than promising copied remote provider bytes; unmapped instance-uploader provenance becomes absent. History, bookmarks and standing reactions travel only under the selected history contract.

The listed restoration effects apply only to archive sections and rows that survive the importer’s validation and rekeying. Open and Closed aliases denote the applicable rows in each state. Absent sections create no subject. Stored conversation visibility and autojoin intent do not imply current upstream membership. Live Current nick, connection progress and cached LIST output are not copied as observed runtime state. Certificate values travel with network configuration; their restored presence does not promise a successful future TLS handshake. Thumbnail bytes can travel, but remote upload bytes and deletion handles do not. Destinations restore with empty secrets and their import defaults. Imported composition has no reply reference. Standing reactions have no withdrawal tombstones.

## Decision points

### Archive contents

Does the archive carry usable message history?

- Usable history present → restore mapped messages and only their mapped bookmarks and standing reactions.
- History absent → restore supported personal configuration and drop history-dependent rows that cannot map.
