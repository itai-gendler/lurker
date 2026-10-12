---
appliesTo:
- type: entity
  id: channel
- type: entity
  id: direct-message
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
  target: server/services/ircManager.ts
---

# Buffer closure preserves history

Close changes visibility, clears draft/pin/favorite associations, lowers join intent and conditionally requests PART. It does not delete retained history immediately. Disconnect, PART and display-clear have different effects.
