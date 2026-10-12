---
appliesTo:
- type: entity
  id: network
- type: entity
  id: channel
- type: entity
  id: direct-message
references:
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# IRC target identity

Channel prefixes are #, &, + and !. Per-network CASEMAPPING folds target identity; bare lowercase matching is not the full contract. Folding and collision reconciliation preserve established buffer identity and associations.
