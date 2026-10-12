---
appliesTo:
- type: entity
  id: network
- type: entity
  id: channel
- type: entity
  id: direct-message
- type: entity
  id: network-log
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
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Mark all connection scope

Mark all walks current IRC-manager connection objects and updates reached retained tails, including reached closed history. It does not enumerate every saved network and excludes the networkless Lurker log.
