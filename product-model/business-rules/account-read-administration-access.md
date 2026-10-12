---
appliesTo:
- type: entity
  id: account
  effect: reads
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Username
  - Pause status
  - Ident
  - Retained history counts
permits:
- actors:
  - administrator
  configuredBy: account
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
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAdmin
---

# Account disclosure requires the stated administrative authority

Only an authenticated Administrator receives the roster, pause, ident and retained-count projection; private conversations and sign-in credential material are not part of that projection.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
