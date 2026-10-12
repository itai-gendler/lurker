---
appliesTo:
- type: entity
  id: instance-settings
  effect: reads
  contexts:
  - place: web::public
  - place: client-api::public
  - place: oauth
  facts:
  - Feature availability
  - Setup status
  - Sign-in availability
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

# Instance settings disclosure is limited to its disclosed public contract

Public disclosed feature/setup/sign-in facts; authenticated bouncer/about/ceiling facts; Admin storage/lockout/policy facts. Changes separately govern network policy, standalone uploader policy and relay policy/status.
