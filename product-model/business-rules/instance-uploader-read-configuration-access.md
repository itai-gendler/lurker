---
appliesTo:
- type: entity
  id: instance-uploader
  effect: reads
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Label
  - Driver
  - Configuration
  - Secret status
  - Enabled
  - Offered to users
  - Default status
  - Managed status
  - Built-in status
permits:
- actors:
  - administrator
  configuredBy: account
references:
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
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

# Instance uploader disclosure requires the stated administrative authority

Only an authenticated Administrator receives the administrative nonsecret configuration projection; managed locked rows also redact protected configuration.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
