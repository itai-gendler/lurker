---
appliesTo:
- type: entity
  id: irc-client
  effect: changes
  contexts:
  - place: irc-bouncer::personal
  facts:
  - Network binding
  from: Attached
permits: []
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Registered bouncer rebinding forbidden

Once downstream registration is Attached, its Network binding cannot be changed. Valid preregistration binding remains supported.
