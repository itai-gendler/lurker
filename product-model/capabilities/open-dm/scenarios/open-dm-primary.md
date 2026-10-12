---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes open dm.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::direct-message
    client:
      place: client-api::personal
  actor: user
- text: For a new private-message target, the Product opens a subject with its supported default facts.
  kind: product
  entities:
  - entity: direct-message
    effect: creates
    facts:
    - Target
    - Visibility
    - Peer presence
    - Read boundary
    - Clear boundary
    - Unread counts
    - Retention override
    - Events
    to: Open
    as: new-direct-message
  - entity: message
    effect: reads
    facts: []
  contexts: *id001
  actor: user
- text: For an existing closed DM target, the Product reopens its visibility and retains its history.
  kind: product
  entities:
  - entity: direct-message
    effect: changes
    as: existing-direct-message
    from: Closed
    to: Open
    facts:
    - Visibility
  contexts:
    web:
      place: web::personal::direct-message
    client:
      place: client-api::personal
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
---

# Open dm

## Trigger

The User invokes open dm.

## Outcome

Direct-message buffer opened or reopened

Opening a new private-message subject creates its default view state; an existing closed subject is reopened.

## Decision points

### Existing subject

Does this target already have a retained private-message subject?

- New target → create the open subject with defaults.
- Existing closed target → reopen that same subject without resetting its retained history.
