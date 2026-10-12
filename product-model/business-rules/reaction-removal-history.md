---
appliesTo:
- type: entity
  id: reaction
- type: entity
  id: message
references:
- kind: code
  role: implementation
  target: server/db/reactions.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
---

# Reaction removal history

Only supported message/action targets with usable upstream identity and negotiated reaction support are eligible. Notices, DCC and encrypted-channel reactions are not supported. Withdrawal uses a retained maximum-timestamp tombstone so stale replay cannot revive an older active reaction.
