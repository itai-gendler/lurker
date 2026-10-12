---
availability:
- place: web::administration
- place: client-api::administration
references:
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
domain: administration-uploaders
---

# Remove instance uploader

Permitted destination removed.

Standalone deletion preserves built-in and current default destinations.
