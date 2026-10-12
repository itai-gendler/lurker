---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes export data.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Owned background export job created/reused and artifact produced
  kind: product
  entities:
  - entity: data-export
    effect: creates
    facts:
    - Requested contents
    - Progress
    - Counts
    - Artifact
    - Error
    - Expires at
    - Downloaded at
    to: Pending
  contexts: *id001
  actor: user
- text: The Product runs the archive build and reports progress.
  kind: product
  entities:
  - entity: data-export
    effect: changes
    facts:
    - Progress
    - Counts
    to: Running
    from: Pending
  contexts: *id001
  actor: user
- text: The Product makes the completed temporary archive available.
  kind: product
  entities:
  - entity: data-export
    effect: changes
    facts:
    - Progress
    - Counts
    - Artifact
    - Expires at
    to: Ready
    from: Running
  contexts: *id001
  actor: user
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
---

# Export data

## Trigger

The User invokes export data.

## Outcome

Owned background export job created/reused and artifact produced

One in-flight owned archive job is created or reused. Background execution reports progress and produces a temporary artifact or records failure.

## Edge cases

- POST uses the active HTTP write guard, including while paused; permitted read/download access has its separate boundary. Sensitive owned configuration can be included in the archive.

## Contract details

The archive can carry portable network/channel connection secrets as plaintext, but omits personal-uploader secret values, local upload deletion handles, account sign-in credentials/roles/pause/ident, draft reply references and reaction-withdrawal tombstones. Imported personal destinations arrive credential-less and require re-entry. Upload records preserve URL/history rather than promising copied remote provider bytes; unmapped instance-uploader provenance becomes absent. History, bookmarks and standing reactions travel only under the selected history contract.