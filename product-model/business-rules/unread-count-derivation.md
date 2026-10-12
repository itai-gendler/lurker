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

# Unread count derivation

Countable conversation messages/actions/notices exclude stamped ignored items under the actual levels and are bounded at 1000. DMs count unread as highlights. Channel highlight rules and replies to self contribute highlights. Network output and the separate Lurker log count their notable output under their own sequences.
