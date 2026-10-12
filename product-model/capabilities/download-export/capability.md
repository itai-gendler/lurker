---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/exports.ts
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/DataPane.vue
domain: data
---

# Download export

Ready owned artifact downloaded.

Only a ready, present owned artifact is returned, with supported range download; readiness conflicts and missing/expired artifacts fail distinctly.
