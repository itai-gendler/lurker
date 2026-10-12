---
kind: primary
routes:
  irc: IRC bouncer
steps:
- text: The User invokes detach irc client.
  kind: actor
  entities:
  - entity: irc-client
    effect: reads
    facts: []
  contexts: &id001
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Downstream attachment ends while upstream remains
  kind: product
  entities:
  - entity: irc-client
    effect: removes
    from: Attached
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Detach irc client

## Trigger

The User invokes detach irc client.

## Outcome

Downstream attachment ends while upstream remains

The downstream client departs; shared upstream connections and retained history remain.
