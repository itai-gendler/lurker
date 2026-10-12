---
appliesTo:
- type: entity
  id: channel
- type: entity
  id: direct-message
- type: entity
  id: network-log
- type: entity
  id: message
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
  target: server/services/ircManager.ts
---

# Clear boundary separation

Clear sets a reversible network-buffer display boundary; show-earlier removes it. Neither operation deletes history or advances read state. Anchored detached history can bypass display clearing; the networkless Lurker log has no mapped clear boundary.
