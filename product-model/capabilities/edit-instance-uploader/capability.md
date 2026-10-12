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

# Edit instance uploader

Permitted instance configuration changed.

Standalone configuration follows managed-row and protected-default restrictions. Responses redact secrets and locked configuration; omitted secrets retain the prior value.
