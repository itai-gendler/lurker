---
appliesTo:
- type: entity
  id: irc-client
- type: entity
  id: network
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Bouncer shared identity

Bound downstream clients use the account’s same upstream connection and current nick. Control mode selects from existing owned networks; it does not create another identity or network.
