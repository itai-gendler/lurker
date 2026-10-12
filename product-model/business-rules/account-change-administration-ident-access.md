---
appliesTo:
- type: entity
  id: account
  effect: changes
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Ident
permits:
- actors:
  - administrator
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
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

# Only the authenticated standalone Administrator assigns a nonconflicting Account ident

Resolve the actual target and the current caller’s authority. The ident path is unavailable in node edition. A supplied nonempty ident must satisfy the supported syntax/length and differ case-insensitively from every other account’s effective ident. Compare against derived effective idents, not just stored overrides. Clearing the override is exempt from this collision test and does not force a reconnect; the new value applies on the next connection.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
