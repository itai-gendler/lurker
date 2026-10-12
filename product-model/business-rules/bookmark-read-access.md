---
appliesTo:
- type: entity
  id: bookmark
  effect: reads
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
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
---

# Bookmark disclosure requires the stated owner or bound entry authority

Owner and owned Message; WS-local versus HTTP guards; dependent parent cleanup.

Unattended retention and closed-subject maintenance consult the relevant saved associations to preserve bookmarked retained content; this is not disclosure to another account.
