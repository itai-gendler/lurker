---
availability:
- place: web::personal
- place: client-api::personal
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

Accepted content stored; owned upload history and URL produced.

Byte classification selects the image or file history subject; each upload creates only the matching subject after provider success. The returned URL addresses stored bytes.
