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

# Upload byte deletion first

Only an owned nonremoved record with a usable deletion path can be deleted. Provider byte deletion happens before history deletion; provider failure leaves history intact. Removing destination configuration can make old records nondeletable.
