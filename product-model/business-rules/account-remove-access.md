---
appliesTo:
- type: entity
  id: account
  effect: removes
  contexts:
  - place: web::administration
  - place: client-api::administration
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

# Only the authenticated Administrator’s current Account authority removes a permitted other Account

Resolve the actual requested target, then compare its identity with the authenticated caller: self-deletion is refused. If the target holds the shipped Administrator role and the current administrator count is at most one, refuse deletion of the only administrator. This comparison uses the actual caller, target and current roster, not another owned account or an invented authorization flag.

An eligible target’s live connections are disposed before its account and dependent data are removed. This handler has no additional standalone-only condition.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
