---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/services/ignoreRulesService.ts
- kind: code
  role: implementation
  target: server/db/ignoredMasks.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
domain: ignores
---

# Remove ignore

Selected matching rules removed.
