---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User requests membership for the selected IRC target.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel-list
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: The Product sends JOIN on the selected live connection and awaits the membership outcome.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  contexts: *id001
  actor: user
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
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
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
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
references:
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
- kind: code
  role: implementation
  target: vue_client/src/components/ChannelListModal.vue
---

# Join channel

## Trigger

The User invokes join channel.

## Outcome

Join requested; confirmed upstream join establishes membership and intent

The request is sent upstream. Confirmation, or the established already-joined path, sets membership and saved intent; an upstream refusal does not manufacture joined state.

## Edge cases

- A newly established subject receives its supported default view facts. Web pending-join confirmation activates the conversation.

## Decision points

### Retained subject

Which subject is established by successful membership?

- No retained subject → create the open subject with its defaults.
- Retained subject → open that same subject and update membership and intent.
