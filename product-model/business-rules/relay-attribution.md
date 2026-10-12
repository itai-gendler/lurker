---
appliesTo:
- type: entity
  id: relay-bot
- type: entity
  id: message
references:
- kind: code
  role: implementation
  target: server/db/relayBots.ts
- kind: code
  role: implementation
  target: server/services/verbs/setRelayBot.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Relay attribution

Only marked scoped nicks use validated envelope templates. Supported unwraps are bounded to four levels and change display attribution while original recorded content remains. Embedded sender text is not an identity proof.
