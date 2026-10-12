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

# Browse uploads

Owned upload history/favorites returned.

Owned history supports the implemented content filters, search, before cursor and favorite projection. Ordinary feeds omit deletion references.
