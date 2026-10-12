---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
---

# Close buffer

Buffer hidden and associated personal state cleaned; history retained.

Closing hides the selected conversation, cleans its draft/pin/favorite associations and lowers join intent. A conditional PART handles possible joined state; retained history is not immediately deleted.
