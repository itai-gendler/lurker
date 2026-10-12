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

# Import data

Eligible validated archive replaces account data.

An eligible validated archive replaces owned data with rekeyed parents and retained content. The account must have zero networks, but prior settings/themes can exist and are replaced.

The archive can carry portable network/channel connection secrets as plaintext, but omits personal-uploader secret values, local upload deletion handles, account sign-in credentials/roles/pause/ident, draft reply references and reaction-withdrawal tombstones. Imported personal destinations arrive credential-less and require re-entry. Upload records preserve URL/history rather than promising copied remote provider bytes; unmapped instance-uploader provenance becomes absent. History, bookmarks and standing reactions travel only under the selected history contract.
