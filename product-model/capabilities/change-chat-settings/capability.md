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

# Change chat settings

Chat preferences change.

Validated overrides in the chat section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
