---
appliesTo:
- type: entity
  id: network
  effect: creates
  contexts:
  - place: irc-bouncer::personal
permits: []
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Bouncer network creation forbidden

Downstream IRC clients cannot create saved networks.
