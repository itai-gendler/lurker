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

# Add ignore

Ignore or exception saved.

A valid ignore or exception with owned scope and supported levels is saved. A duplicate specification refreshes its lifetime.
