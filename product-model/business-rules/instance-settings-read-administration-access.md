---
appliesTo:
- type: entity
  id: instance-settings
  effect: reads
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Edition
  - Feature availability
  - Network policy
  - Uploader policy
  - Retention ceilings
  - Notification transports
  - Relay opt-in
  - Relay status
  - Storage measurements
  - Versions
  - Login policy
  - Blocked sign-ins
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

# Instance settings disclosure requires the stated administrative authority

Public disclosed feature/setup/sign-in facts; authenticated bouncer/about/ceiling facts; Admin storage/lockout/policy facts. Changes separately govern network policy, standalone uploader policy and relay policy/status.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
