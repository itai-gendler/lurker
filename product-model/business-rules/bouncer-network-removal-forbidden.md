---
appliesTo:
- type: entity
  id: network
  effect: removes
  contexts:
  - place: irc-bouncer::personal
permits: []
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Bouncer network removal forbidden

Downstream clients cannot remove saved networks or their retained histories.
