---
appliesTo:
- type: entity
  id: irc-client
- type: entity
  id: network
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
---

# Bouncer detach preserves upstream

QUIT/downstream departure removes the attachment and its presence contribution while leaving the always-on upstream and saved data intact.
