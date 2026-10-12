---
appliesTo:
- type: entity
  id: bookmark
  effect: creates
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
references:
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
---

# Bookmark creation requires the stated owner or bound entry authority

Owner and owned Message; WS-local versus HTTP guards; dependent parent cleanup.
