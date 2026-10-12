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
---

# Change appearance settings

Appearance overrides/theme selection change.

Validated overrides in the appearance section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
