---
kind: exception
routes:
  web-public: Web entry
steps:
- text: The User requests local shared-upload bytes whose object key is absent.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public
  actor: user
- text: For the selected content class, the Product applies the selected-image or selected-file operation.
    Missing local object key returns failure
  kind: product
  entities: []
  contexts: *id001
  actor: user
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

# Open shared upload missing key

## Trigger

The User requests local shared-upload bytes whose object key is absent.

## Outcome

Missing local object key returns failure
