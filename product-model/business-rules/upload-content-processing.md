---
appliesTo:
- type: entity
  id: image-upload
- type: entity
  id: file-upload
references:
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
---

# Upload content processing

Magic bytes determine image/media/text acceptance under effective size, driver and content policy. Static images can be resized and metadata scrubbed. The evidenced GIF, animated WebP and APNG paths preserve animation; this is not a universal animation-container promise. SVG policy, supported media metadata handling and text passthrough keep their actual contract. Thumbnail failure does not invent a thumbnail or necessarily fail successful provider storage.
