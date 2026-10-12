---
appliesTo:
- type: entity
  id: message
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Offline history

Stored history queries check ownership and retention, not live IRC connectivity. Fetching a known shell does not JOIN, reopen or connect it.
