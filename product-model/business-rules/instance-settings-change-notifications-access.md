---
appliesTo:
- type: entity
  id: instance-settings
  effect: changes
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Relay opt-in
  - Relay status
permits:
- actors:
  - administrator
  configuredBy: account
references:
- kind: code
  role: implementation
  target: server/routes/config.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAdmin
---

# Instance settings changes require the stated administrative authority

Only an authenticated unpaused Administrator changes the supported relay opt-in/status policy. Registration/delivery require opt-in, while explicit administrative checking may contact the relay when delivery is disabled; stale generations are discarded.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
