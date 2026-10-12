---
kind: primary
result: achieved
routes:
  web: Web
steps:
- text: The User selects a listed target and submits JOIN from the directory.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts:
    - Listed channels
  contexts:
    web:
      place: web::personal::channel-list
  actor: user
  capability: join-channel
- text: The Product sends JOIN on the selected live connection and awaits the membership outcome.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  contexts:
    web:
      place: web::personal::channel-list
  actor: user
  capability: join-channel
- text: When upstream confirms a previously absent subject, the Product opens it with its initial facts and accepted
    join intent.
  kind: product
  entities:
  - entity: channel
    effect: creates
    as: new-channel
    to: Open
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
  contexts:
    web:
      place: web::personal::channel-list
  actor: user
  capability: join-channel
- text: When confirmation or observed existing membership addresses a retained subject, the Product opens it and
    saves accepted join intent.
  kind: product
  entities:
  - entity: channel
    effect: changes
    as: existing-channel
    facts:
    - Visibility
    - Joined status
    - Autojoin
    - Channel key
  contexts:
    web:
      place: web::personal::channel-list
  actor: user
  capability: join-channel
- text: The web pending-join confirmation activates the confirmed conversation.
  kind: product
  entities: []
  contexts:
    web:
      place: web::personal::channel-list
  actor: user
  capability: join-channel
- text: The User reads the activated channel conversation.
  kind: actor
  entities:
  - entity: channel
    effect: reads
    as: new-channel
    facts: []
  - entity: channel
    effect: reads
    as: existing-channel
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
  actor: user
  capability: browse-messages
- text: The Product returns the selected destination’s retained conversation information.
  kind: product
  entities:
  - entity: message
    effect: reads
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
  contexts: *id001
  actor: user
  capability: browse-messages
references:
- kind: code
  role: implementation
  target: vue_client/src/components/ChannelListModal.vue
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/verbs/joinChannel.ts
---

# Channel join to conversation achieved

## Trigger

Join a channel and arrive in its usable conversation.

## Outcome

Upstream join confirmation activates the conversation, where the carried person can browse its retained content.

## Decision points

### Retained subject

Does successful membership establish a new or existing conversation?

- New subject → its default facts are created before activation.
- Retained subject → its visibility and accepted membership are updated before activation.
