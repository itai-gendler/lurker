---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove network.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: The Product disposes the selected connection and removes its saved configuration with any dependent records
    in their current listed states.
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
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/index.ts
---

# Remove network

## Trigger

The User invokes remove network.

## Outcome

Connection disposed; network and dependent data removed

The live connection is disposed before the network and its dependent retained data are deleted.

## Edge cases

- This removes owned network history; disconnect instead retains it.
