---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/uploads.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
---

# Favorite upload

Owned upload starred.

The selected owned image or file’s star changes. The endpoint can update a removed owned row even though favorite feeds exclude removed rows.
