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

# Delete upload

Provider deletion succeeds before history removal.

Only the selected image or file row is removed, after its configured provider deletion succeeds.
