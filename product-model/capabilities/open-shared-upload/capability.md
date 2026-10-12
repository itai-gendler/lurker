---
availability:
- place: web::public
references:
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/routes/uploads.ts
- kind: code
  role: implementation
  target: server/services/uploadProviders/local.ts
---

# Open shared upload

Valid local key-addressed public bytes returned.

A valid local key returns only the matching stored object’s bytes through the public route. Inline content, forced-download, CSP, nosniff and range handling follow the safe supported content contract.
