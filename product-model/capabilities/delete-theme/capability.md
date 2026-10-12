---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/services/themesService.ts
- kind: code
  role: implementation
  target: server/db/themes.ts
domain: themes
---

# Delete theme

Saved theme removed.

Deletion removes the saved theme and resets an appearance selection pointing at that theme.
