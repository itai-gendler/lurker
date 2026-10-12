---
appliesTo:
- type: capability
  id: connect-network
- type: capability
  id: disconnect-network
- type: capability
  id: reconnect-network
- type: capability
  id: remove-network
- type: capability
  id: set-away
- type: capability
  id: clear-away
- type: entity
  id: lurker-log
references:
- kind: code
  role: implementation
  target: server/services/systemLog.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/server.ts
- kind: code
  role: implementation
  target: server/db/systemMessages.ts
---

# Lurker events recorded

The inspected connection launch/adoption, stop/disposal and real away/back change paths record account-private Product events in the Lurker log. Server lifecycle and explicitly global notices use its global view. Each account receives only global lines plus its own private lines and keeps its read boundary in the separate event sequence. A no-op or refused request is not promised an event. Source-specific connection/adoption and autojoin messages remain distinct from retained upstream server output in the Network log.
