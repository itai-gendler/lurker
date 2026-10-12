---
appliesTo:
- type: entity
  id: invite
  effect: reads
permits:
- actors:
  - user
  - administrator
references:
- kind: code
  role: implementation
  target: server/db/invites.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Invite disclosure requires the stated owner or bound entry authority

Admin create/remove/roster; valid invitation proof reads limited entry facts and consumes once.
