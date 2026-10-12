---
appliesTo:
- type: entity
  id: bookmark
  effect: removes
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

# Bookmark removal requires the stated owner or bound entry authority

Owner and owned Message; WS-local versus HTTP guards; dependent parent cleanup.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
