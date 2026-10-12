---
kind: path
routes:
  irc: IRC bouncer
steps:
- text: The User requests BOUNCER LISTNETWORKS from the registered account control connection.
  kind: actor
  entities:
  - entity: account
    effect: reads
    facts: []
  actor: user
  contexts:
    irc:
      place: irc-bouncer::personal
- text: The Product returns one supported wire projection for each selectable personal connection configuration.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Name
    - Current nick
    - Connection state
    - Connection configuration
  actor: user
  contexts:
    irc:
      place: irc-bouncer::personal
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts#sendNetworkList
- kind: code
  role: implementation
  target: server/services/bouncer.ts#networkAttrs
- kind: code
  role: implementation
  target: server/db/networks.ts#listNetworksForUser
---

# Browse networks through bouncer control

## Trigger

The registered control client sends BOUNCER LISTNETWORKS using its supported negotiated extension.

## Outcome

The client receives name, connection state, host, port, TLS, current/fallback nickname and any current connection error. Batch wrapping and batch tags follow the negotiated batch extension. A notify client can receive the initial list and subsequent attribute changes without a separate request. This projection does not disclose proxy/startup/authentication preferences or offered Network presets.

## Edge cases

- An account with no networks receives an empty list and setup guidance; no network is manufactured.
- An unsupported BOUNCER command or missing extension produces the established FAIL response. Control mode carries no channel traffic or arbitrary network-management authority.
