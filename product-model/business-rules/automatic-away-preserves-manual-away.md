---
appliesTo:
- type: entity
  id: network
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
---

# Automatic away preserves manual away

Counted absence can establish automatic away after the applicable enabled delay, falling back to thirty seconds where configured behavior does so. It does not overwrite manual away. Counted presence return clears applicable automatic away only.
