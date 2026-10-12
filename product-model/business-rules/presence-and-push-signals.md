---
appliesTo:
- type: entity
  id: irc-client
- type: entity
  id: network
- type: entity
  id: account
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
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
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
---

# Presence and push signals

Visible WebSocket presence and bound non-away IRC clients contribute according to the automatic-away contract; control mode is not network presence. Phone-push suppression uses visible WebSocket presence rather than simply any bouncer attachment.
