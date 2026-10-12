---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/uploaders.ts
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/services/uploadProviders/resolve.ts
domain: uploads
---

# Edit personal uploader

Owned configuration changed.

Personal destination configuration follows the supported driver and creation policy. Configuration responses omit secret values; omitted replacement secrets retain existing values.
