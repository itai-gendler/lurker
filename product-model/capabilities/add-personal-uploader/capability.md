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

# Add personal uploader

Allowed owned destination configuration created.

Personal destination configuration follows the supported driver and creation policy. Configuration responses omit secret values; omitted replacement secrets retain existing values.
