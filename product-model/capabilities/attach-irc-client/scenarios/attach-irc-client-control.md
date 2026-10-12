---
kind: path
routes:
  irc-registration: IRC registration
  irc: IRC bouncer
steps:
- text: The User registers an IRC client with no configured upstream binding when control-mode selection applies.
  kind: actor
  entities:
  - entity: irc-client
    effect: reads
    facts: []
  contexts: &id001
    irc-registration:
      place: irc-bouncer::public
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Account control mode established without creating a network
  kind: product
  entities:
  - entity: irc-client
    effect: creates
    facts:
    - Registration
    - Network binding
    - Negotiated extensions
    - Credential association
    - Presence contribution
    to: Registering
  - entity: account
    effect: reads
    facts: []
  - entity: network
    effect: reads
    facts: []
  contexts: *id001
  actor: user
- text: The Product completes downstream registration in the selected binding.
  kind: product
  entities:
  - entity: irc-client
    effect: changes
    facts:
    - Registration
    - Network binding
    - Negotiated extensions
    - Presence contribution
    to: Attached
    from: Registering
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Attach irc client control

## Trigger

The User registers an IRC client with no network binding when control-mode selection applies.

## Outcome

Account control mode established without creating a network
