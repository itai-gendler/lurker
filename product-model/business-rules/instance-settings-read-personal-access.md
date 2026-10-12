---
appliesTo:
- type: entity
  id: instance-settings
  effect: reads
  contexts:
  - place: web::personal
  - place: client-api::personal
  - place: irc-bouncer::personal
  facts:
  - Feature availability
  - Retention ceilings
  - Notification transports
  - Relay opt-in
  - Bouncer connection details
  - Versions
  - Edition
permits:
- actors:
  - user
  - administrator
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
---

# Instance settings disclosure requires the stated owner or bound entry authority

Public disclosed feature/setup/sign-in facts; authenticated bouncer/about/ceiling facts; Admin storage/lockout/policy facts. Changes separately govern network policy, standalone uploader policy and relay policy/status.
