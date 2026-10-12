---
appliesTo:
- type: entity
  id: file-upload
  effect: reads
  contexts:
  - place: web::public
  facts:
  - URL
  - Content type
  - Byte size
permits:
- actors:
  - user
  - administrator
  configuredBy: file-upload
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
references:
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
- kind: code
  role: implementation
  target: server/routes/localUploads.ts
---

# Public local upload bytes require the exact retained standalone key

The selected upload configures disclosure through the exact addressed public local-upload key and its existing disk object. On standalone, the byte-serving route returns that object and its supported response metadata without account sign-in. Malformed keys and absent disk objects return 404. The handler does not consult upload-history Removal status; removal of account/history metadata alone is not a promise to make a still-existing local object inaccessible. This grant does not expose the owner’s upload roster, provider credentials or deletion handle. Provider-hosted public URLs remain external contracts.
