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

# Change input bar settings

Input preferences change.

Validated overrides in the input bar section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
