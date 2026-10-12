---
appliesTo:
- type: entity
  id: account
  effect: reads
  contexts:
  - place: web::personal
  - place: client-api::personal
  facts:
  - Username
  - Sign-in methods
  - Pause status
  - Ident
  - Appearance settings
  - Chat settings
  - Event settings
  - Input bar settings
  - Upload settings
  - Notification settings
  - Away settings
  - Data settings
permits:
- related:
  - verb: has-account
    entity: user
- related:
  - verb: has-account
    entity: administrator
- unattended: true
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
---

# Account disclosure requires the stated owner or bound entry authority

Only the acting account receives its private information through an accepted ordinary session or OAuth path. Administrative privilege alone never grants another account’s private settings.

Unattended reads consult the recipient’s notification/away preferences for the eligible delivery policy; they do not expose private preferences to unrelated people.
