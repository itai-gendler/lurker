---
availability:
- place: web::public
- place: client-api::public
references:
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/db/invites.ts
---

# Accept invite

Valid invitation is consumed; account and session created.

The successful password path consumes the invitation and issues account access. Web success carries the person into chat; passkey redemption is separately exposed through the client API.
