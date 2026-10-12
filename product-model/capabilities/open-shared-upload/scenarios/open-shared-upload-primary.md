---
kind: primary
routes:
  web-public: Web entry
steps:
- text: The User invokes open shared upload.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public
  actor: user
- text: For the selected content class, the Product applies the selected-image or selected-file operation. Valid
    local key-addressed public bytes returned
  kind: product
  entities:
  - entity: image-upload
    effect: reads
    facts:
    - URL
    - Content type
    - Byte size
  - entity: file-upload
    effect: reads
    facts:
    - URL
    - Content type
    - Byte size
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
- kind: code
  role: implementation
  target: server/routes/localUploads.ts
---

# Open shared upload

## Trigger

The User invokes open shared upload.

## Outcome

Valid local key-addressed public bytes returned

A valid local key returns only the matching stored object’s bytes through the public route. Inline content, forced-download, CSP, nosniff and range handling follow the safe supported content contract.

## Edge cases

- Missing keys fail. Public retrieval does not disclose personal upload history or provider deletion credentials.

## Contract details

The local route checks the addressed disk object, without consulting upload-history ownership or Removal status. A forced-download filename uses the random storage key, rather than disclosing the original upload-history filename. Removing history metadata alone does not guarantee public bytes are gone.
