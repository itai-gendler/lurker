---
appliesTo:
- type: entity
  id: invite
  effect: changes
permits:
- actors:
  - user
  - administrator
  configuredBy: invite
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

# Only a valid presented invitation is consumed during supported entry

The Invite-configured grant selects the exact presented invitation proof, requires it available and unexpired, and consumes it once as its account entry succeeds. Unknown, expired or consumed proof cannot change an invitation. It grants no general invitation editing authority. Creation and roster removal require their separate administrative grants.
