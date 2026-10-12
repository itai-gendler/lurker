---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
domain: uploads
---

# Change uploads settings

Processing/default-destination choices change.

Validated overrides in the uploads section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
