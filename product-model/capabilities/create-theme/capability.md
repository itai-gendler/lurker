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

# Create theme

Named theme snapshot saved.

A valid named values snapshot is saved under the account’s theme-name and count limits.
