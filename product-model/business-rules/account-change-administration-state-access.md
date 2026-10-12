---
appliesTo:
- type: entity
  id: account
  effect: changes
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Pause status
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

# Only the authenticated Administrator’s current Account authority pauses or resumes an eligible target

The actual pause/resume request is permitted only in standalone edition after the caller’s administrative authentication and write guard. Resolve the requested account and compare its identity to the authenticated caller for pause: self-pause is refused before the already-paused no-op. An eligible other account may be paused idempotently; the pause flag is set before live IRC/bouncer suspension.

Resume has no self-target comparison in the handler. It requires the same current caller’s administrative write authority and an existing target. An already-active target returns the established no-op; otherwise clear pause and initialize configured connections. The caller’s own paused account cannot bypass requireAuth by requesting resume.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
