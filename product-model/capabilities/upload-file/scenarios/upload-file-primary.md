---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes upload file.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: For the selected content class, the Product records the image result or the file result after provider
    success. Accepted content stored; owned upload history and URL produced
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

# Upload file

## Trigger

The User invokes upload file.

## Outcome

Accepted content stored; owned upload history and URL produced

Byte classification selects the image or file history subject; each upload creates only the matching subject after provider success. The returned URL addresses stored bytes.

## Edge cases

- The effective size limit combines transport, destination and account limits. Driver/content policy gates acceptance.
- Static image processing can resize and strip metadata; evidenced GIF/WebP/APNG paths preserve animation. SVG handling and media processing keep their supported policy boundaries; text is passed through.
- Image thumbnails are best effort. Provider failures do not create successful history records. FILEHOST accepts its distinct Basic or bearer credential paths over HTTP, not cookies.

## Decision points

### Content classification

Which accepted history subject describes these bytes?

- Image bytes → The stored URL returns with image dimensions and any thumbnail.
- Accepted media or text bytes → The stored URL returns with file facts without image-only fields.
