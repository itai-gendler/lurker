---
appliesTo:
- type: entity
  id: invite
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

# Invite single use

Successful redemption consumes the invitation exactly once. Unknown, expired and consumed proofs refuse account admission. Deleting its row does not remove an already-admitted member.
