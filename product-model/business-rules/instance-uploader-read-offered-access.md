---
appliesTo:
- type: entity
  id: instance-uploader
  effect: reads
  contexts:
  - place: web::personal
  - place: client-api::personal
  facts:
  - Label
  - Driver
  - Enabled
  - Offered to users
  - Default status
permits:
- actors:
  - user
  - administrator
references:
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
---

# Instance uploader disclosure requires the stated owner or bound entry authority

Only signed-in account users receive offered nonsecret metadata for enabled permitted instance destinations. This never reveals provider credentials or managed private configuration.
