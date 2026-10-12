---
appliesTo:
- type: entity
  id: theme
- type: entity
  id: account
references:
- kind: code
  role: implementation
  target: server/db/themes.ts
- kind: code
  role: implementation
  target: server/services/themesService.ts
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

# Theme values and pointers

Saved themes have validated name/value/count limits and name-conflict refusal. Deleting a selected saved theme resets its appearance pointer. Built-in presets are shipped vocabulary rather than saved theme instances.
