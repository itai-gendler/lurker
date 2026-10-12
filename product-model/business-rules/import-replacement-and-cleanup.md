---
appliesTo:
- type: entity
  id: account
- type: entity
  id: network
- type: entity
  id: theme
- type: entity
  id: message
references:
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
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
  target: server/db/themes.ts
- kind: code
  role: implementation
  target: server/services/themesService.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
---

# Import replacement and cleanup

Import requires zero networks and a valid supported archive. Validation precedes replacement; preferences/themes can already exist and are replaced. Phased parent/content/dependent import rekeys identities and clamps or drops invalid retention settings under policy. Partial-failure cleanup removes imported data but does not restore original preferences/themes. Web success resets client state and routes to chat.
