---
appliesTo:
- type: entity
  id: message
- type: entity
  id: network-log
- type: entity
  id: lurker-log
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
- kind: code
  role: implementation
  target: server/services/systemLog.ts
---

# History resume contiguity

WS bounded latest/before/after/around and resume retain contiguous slices. Resume gaps use bounded replacement rather than unsafe append. The Lurker log has its own sequence and replaces its slice. Stale request tokens do not overwrite newer web state. Detached historical views can drop live rows until return-to-present replaces the window.
