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
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
- kind: code
  role: implementation
  target: server/services/exportService.ts
domain: data
---

# Export data

Owned background export job created/reused and artifact produced.

One in-flight owned archive job is created or reused. Background execution reports progress and produces a temporary artifact or records failure.

The archive can carry portable network/channel connection secrets as plaintext, but omits personal-uploader secret values, local upload deletion handles, account sign-in credentials/roles/pause/ident, draft reply references and reaction-withdrawal tombstones. Imported personal destinations arrive credential-less and require re-entry. Upload records preserve URL/history rather than promising copied remote provider bytes; unmapped instance-uploader provenance becomes absent. History, bookmarks and standing reactions travel only under the selected history contract.
