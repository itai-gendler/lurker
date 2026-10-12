---
kind: path
routes:
  client: Client API
steps:
- text: The User uploads bytes through the advertised HTTP FILEHOST contract.
  kind: actor
  entities: []
  contexts: &id001
    client:
      place: client-api::personal
  actor: user
- text: For the selected content class, the Product records the image result or the file result after provider
    success. Advertised HTTP FILEHOST accepts its supported credentials and uploads bytes
  kind: product
  entities:
  - entity: image-upload
    effect: creates
    facts:
    - Filename
    - URL
    - Content type
    - Byte size
    - Dimensions
    - Thumbnail
    - Deletion reference
    - Favorite status
    - Removal status
  - entity: file-upload
    effect: creates
    facts:
    - Filename
    - URL
    - Content type
    - Byte size
    - Deletion reference
    - Favorite status
    - Removal status
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/uploads.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/routes/filehost.ts
---

# Upload file filehost

## Trigger

The User uploads bytes through the advertised HTTP FILEHOST contract.

## Outcome

Advertised HTTP FILEHOST accepts its supported credentials and uploads bytes

## Decision points

### Content classification

Which accepted history subject describes these bytes?

- Image bytes → The stored URL returns with image dimensions and any thumbnail.
- Accepted media or text bytes → The stored URL returns with file facts without image-only fields.
