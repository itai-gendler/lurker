---
appliesTo:
- type: entity
  id: channel
- type: entity
  id: direct-message
- type: entity
  id: network-log
- type: entity
  id: lurker-log
references:
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
- kind: code
  role: implementation
  target: server/services/systemLog.ts
---

# Read boundary monotonicity

Accepted shared markers use the maximum of existing and submitted boundaries. WS requires positive finite IDs but does not prove integer, tail bounds or submitted-buffer membership. Bouncer timestamps resolve to retained rows; queries/nonmoving results respond only to their requester.
