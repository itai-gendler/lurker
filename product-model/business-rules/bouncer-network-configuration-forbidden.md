---
appliesTo:
- type: entity
  id: network
  effect: changes
  contexts:
  - place: irc-bouncer::personal
  facts:
  - Connection configuration
  - Authentication
  - Connection preferences
  - Startup channels
permits: []
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Bouncer network configuration forbidden

Downstream clients cannot edit saved connection configuration, authentication, preferences or startup-channel lists. Bound nick/away operations are separate supported IRC actions.
